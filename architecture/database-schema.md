# Database Schema

Phase 1 core tables. This reflects the actual AverisOS data model — the traceability graph plus the work-ownership model it depends on — not a generic starter schema. Postgres 15+.

See [ADR-011](../decisions/adr-011-graph-modeling.mdx) for why the graph is modeled this way, and [Work Management Model](../planning/work-management.mdx) for the full ownership/assignment data model this summarizes.

## Users

```sql
CREATE TABLE users (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  email VARCHAR(255) UNIQUE NOT NULL,
  password_digest VARCHAR(255) NOT NULL,
  first_name VARCHAR(255),
  last_name VARCHAR(255),
  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW(),
  deleted_at TIMESTAMP
);

CREATE INDEX idx_users_email ON users(email);
```

## Projects & Teams

```sql
CREATE TABLE projects (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  owner_user_id UUID NOT NULL REFERENCES users(id),
  name VARCHAR(255) NOT NULL,
  status VARCHAR(50) NOT NULL DEFAULT 'draft', -- draft | ready_for_work
  confidential BOOLEAN NOT NULL DEFAULT FALSE,
  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW()
);

CREATE TABLE teams (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  name VARCHAR(255) NOT NULL,
  created_at TIMESTAMP DEFAULT NOW()
);

CREATE TABLE team_memberships (
  team_id UUID NOT NULL REFERENCES teams(id),
  user_id UUID NOT NULL REFERENCES users(id),
  role VARCHAR(50) NOT NULL, -- admin | editor | viewer
  PRIMARY KEY (team_id, user_id)
);

CREATE TABLE project_teams (
  project_id UUID NOT NULL REFERENCES projects(id),
  team_id UUID NOT NULL REFERENCES teams(id),
  access_level VARCHAR(50) NOT NULL, -- view | contribute | admin
  PRIMARY KEY (project_id, team_id)
);
```

## Artifacts (Traceability Core)

```sql
CREATE TABLE artifacts (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  project_id UUID NOT NULL REFERENCES projects(id),
  type VARCHAR(50) NOT NULL, -- requirement | feature | code | test | release | ...
  title VARCHAR(500) NOT NULL,
  description TEXT,
  owner_id UUID REFERENCES users(id),
  status VARCHAR(50) NOT NULL DEFAULT 'draft', -- draft | active | archived
  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW(),
  archived_at TIMESTAMP
);

CREATE INDEX idx_artifacts_project ON artifacts(project_id);
CREATE INDEX idx_artifacts_type ON artifacts(type);
```

## Artifact Relationships & Closure (Graph)

The adjacency list (`artifact_relationships`) is the source of truth for what a user actually linked. The closure table (`artifact_closures`) is a derived, synchronously-maintained index of every transitive pair, so impact analysis reads in O(1) instead of walking a recursive CTE per request. See [ADR-011](../decisions/adr-011-graph-modeling.mdx) for the full rationale and revisit trigger.

```sql
CREATE TABLE artifact_relationships (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  source_artifact_id UUID NOT NULL REFERENCES artifacts(id),
  target_artifact_id UUID NOT NULL REFERENCES artifacts(id),
  relationship_type VARCHAR(50) NOT NULL, -- implements | validates | depends_on | related_to | blocks
  created_by UUID NOT NULL REFERENCES users(id),
  notes TEXT,
  created_at TIMESTAMP DEFAULT NOW(),
  UNIQUE (source_artifact_id, target_artifact_id, relationship_type)
);

CREATE TABLE artifact_closures (
  ancestor_id UUID NOT NULL REFERENCES artifacts(id),
  descendant_id UUID NOT NULL REFERENCES artifacts(id),
  depth INTEGER NOT NULL, -- 0 = self, 1 = direct, 2+ = transitive
  PRIMARY KEY (ancestor_id, descendant_id)
);

CREATE INDEX idx_closures_descendant ON artifact_closures(descendant_id);
```

## Work Assignment (Phase 1 — ownership only, no sprint ceremony)

Phase 1 keeps team/individual ownership and the pull/push assignment flow, because traceability without ownership context is just orphaned artifacts (see [PRD §23: "Why Work Management is Phase 1"](../planning/prd.mdx)). Formal sprint planning and multi-methodology workflow (Kanban boards, WIP limits, Waterfall stage gates) are **deferred to Phase 2** — see [Work Management Model](../planning/work-management.mdx) for the full reasoning. `artifacts.status` uses a simplified set in Phase 1: `unassigned → team_backlog → in_progress → completed` (no `sprint` state until Phase 2 introduces the `sprints` table).

```sql
CREATE TABLE artifact_team_assignments (
  artifact_id UUID NOT NULL REFERENCES artifacts(id),
  team_id UUID NOT NULL REFERENCES teams(id),
  source VARCHAR(50) NOT NULL, -- team_self | owner_flagged | management_assigned
  assigned_at TIMESTAMP DEFAULT NOW(),
  accepted_at TIMESTAMP, -- null if management_assigned
  PRIMARY KEY (artifact_id, team_id)
);

CREATE TABLE artifact_user_assignments (
  artifact_id UUID NOT NULL REFERENCES artifacts(id),
  user_id UUID NOT NULL REFERENCES users(id),
  role VARCHAR(50) NOT NULL, -- assignee | reviewer | owner
  assigned_at TIMESTAMP DEFAULT NOW(),
  PRIMARY KEY (artifact_id, user_id, role)
);

CREATE TABLE flagged_items (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  artifact_id UUID NOT NULL REFERENCES artifacts(id),
  from_team_id UUID REFERENCES teams(id),
  to_team_id UUID NOT NULL REFERENCES teams(id),
  status VARCHAR(50) NOT NULL DEFAULT 'pending', -- pending | accepted | reassigned | triaged
  created_at TIMESTAMP DEFAULT NOW()
);

CREATE TABLE triage_pool (
  artifact_id UUID PRIMARY KEY REFERENCES artifacts(id),
  conflicting_teams JSONB NOT NULL,
  assigned_by UUID REFERENCES users(id),
  resolved_team_id UUID REFERENCES teams(id),
  resolved_at TIMESTAMP
);
```

## Indexing Summary

| Table | Index | Purpose |
|-------|-------|---------|
| `users` | `email` | Login queries |
| `artifacts` | `project_id`, `type` | Project scoping, filtering by type |
| `artifact_closures` | `descendant_id` (in addition to PK on `ancestor_id, descendant_id`) | "What points to X" queries in addition to "what does X reach" |
| `artifact_team_assignments` | PK on `(artifact_id, team_id)` | Team backlog queries |

## Migrations

Migrations live in `backend/db/migrate/`. `artifact_closures` writes happen inside the same transaction as `artifact_relationships` writes (see [ADR-006](../decisions/adr-006-event-dispatcher.mdx) — Phase 1 is synchronous throughout), inside the `LinkArtifacts`/`UnlinkArtifacts` Command operations.

## Backup Strategy

- Daily automated backups
- 30-day retention
- Point-in-time recovery available
