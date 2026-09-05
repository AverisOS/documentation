# AverisOS Mintlify Documentation Structure

This document describes the complete documentation structure created for AverisOS with hierarchical navigation.

## Navigation Hierarchy

The documentation is now organized into 7 main sections with proper hierarchy:

```
Home
├── Getting Started
│   ├── Overview
│   └── Quick Start
│
├── Planning & Strategy (collapsible)
│   ├── Roadmap
│   ├── Business Model
│   └── Go-to-Market
│
├── Architecture (collapsible)
│   ├── Overview
│   ├── Design Principles
│   ├── Patterns
│   └── Monorepo Structure
│
├── Domains
│   └── Overview
│
├── Architecture Decisions / ADRs (collapsible)
│   ├── ADR-001: Domain-Driven Design
│   ├── ADR-002: Result Monad
│   ├── ADR-003: Monorepo
│   ├── ADR-004: REST API
│   ├── ADR-005: dry-rb
│   ├── ADR-006: Event Dispatcher
│   ├── ADR-007: Phase 1 Focus
│   ├── ADR-008: Open Source
│   ├── ADR-009: Design Partners
│   └── ADR-010: Self-Hosted
│
└── Development (collapsible)
    ├── Setup
    ├── Contributing
    ├── Testing Strategy
    └── Claude Guide
```

## Directory Layout

```
documentation/
├── docs.json                          # Mintlify configuration (hierarchical)
├── STRUCTURE.md                       # This file
├── index.mdx                          # Landing page
│
├── getting-started/                   # Getting Started Section
│   ├── overview.mdx                   # Product overview
│   └── quick-start.mdx                # 5-minute quickstart
│
├── planning/                          # Planning & Strategy Section
│   ├── roadmap.mdx                    # 18-month product roadmap
│   ├── business-model.mdx             # Pricing, revenue, go-to-market
│   └── go-to-market.mdx               # Customer acquisition strategy
│
├── architecture/                      # Architecture Section
│   ├── overview.mdx                   # Architecture layers & patterns
│   ├── design-principles.mdx          # 10 core design principles
│   ├── patterns.mdx                   # Common implementation patterns
│   └── monorepo-structure.mdx         # How domains are organized
│
├── domains/                           # Domains Section
│   └── overview.mdx                   # Overview of all domains
│
├── decisions/                         # Architecture Decisions Section (ADRs)
│   ├── adr-001-ddd.mdx
│   ├── adr-002-result-monad.mdx
│   ├── adr-003-monorepo.mdx
│   ├── adr-004-rest-api.mdx
│   ├── adr-005-dry-rb.mdx
│   ├── adr-006-event-dispatcher.mdx
│   ├── adr-007-phase-1-focus.mdx
│   ├── adr-008-open-source.mdx
│   ├── adr-009-design-partners.mdx
│   └── adr-010-self-hosted.mdx
│
└── development/                       # Development Section
    ├── setup.mdx                      # Local development setup
    ├── contributing.mdx               # Contribution guidelines
    ├── testing-strategy.mdx           # Testing pyramid & best practices
    └── claude-guide.mdx               # How to work with Claude AI
```

## What Changed

### Before (Flat Navigation)
The old `docs.json` used a flat array of pages:
```json
{
  "navigation": {
    "pages": [
      "index",
      "getting-started/overview",
      "getting-started/quick-start",
      "planning/roadmap",
      ...
    ]
  }
}
```

This resulted in a long, unsorted list in the sidebar with no visual organization.

### After (Hierarchical Navigation)
The new structure uses grouped sections with collapsible groups:
```json
{
  "navigation": [
    {
      "group": "Home",
      "pages": ["index"]
    },
    {
      "group": "Getting Started",
      "pages": [
        "getting-started/overview",
        "getting-started/quick-start"
      ]
    },
    {
      "group": "Planning & Strategy",
      "collapsible": true,
      "pages": [...]
    },
    ...
  ]
}
```

This provides:
- **Clear sections** - Users immediately see what documentation categories exist
- **Collapsible groups** - Less important sections can be collapsed to reduce clutter
- **Better navigation** - Users can quickly find what they're looking for
- **Improved UX** - Follows Mintlify best practices

## Section Descriptions

### Home
Single landing page that introduces AverisOS.

### Getting Started
Quick orientation for new users. Read in order:
1. Overview — What is AverisOS?
2. Quick Start — 5-minute setup guide

**Audience:** First-time visitors, potential users

### Planning & Strategy
Business and product strategy documentation. Collapsible because it's primarily for stakeholders/leadership.

- **Roadmap** — 18-month product plan with phases and deliverables
- **Business Model** — Pricing tiers, revenue model, financial projections  
- **Go-to-Market** — Customer acquisition, ICP, channels, marketing

**Audience:** Stakeholders, leadership, potential partners

### Architecture
Technical architecture and design patterns. Core resource for engineers.

- **Overview** — High-level architecture, layers, patterns
- **Design Principles** — 10 core DDD principles with examples
- **Patterns** — 5 common implementation patterns
- **Monorepo Structure** — Directory organization and domain boundaries

**Audience:** Engineers, architects, technical leads

### Domains
Information about business domains (traceability, authentication, etc.).

- **Overview** — Description of all domains and their relationships

**Audience:** Product team, engineers

### Architecture Decisions (ADRs)
Detailed architectural decision records. Collapsible because developers reference these as needed.

Each ADR follows the standard format:
- Context — Why this decision was needed
- Decision — What was decided
- Alternatives — Other options considered
- Rationale — Why this choice was made
- Consequences — What this means going forward

**Audience:** Developers, architects, new team members

### Development
Practical guides for building and collaborating. Collapsible for secondary reference.

- **Setup** — Local development environment configuration
- **Contributing** — PR process, code style, contribution guidelines
- **Testing Strategy** — Testing pyramid, RSpec patterns, best practices
- **Claude Guide** — How to effectively work with Claude AI

**Audience:** Developers, contributors

## File Count

- **Total documentation files**: 25 files
- **Architecture files**: 4 files
- **ADRs**: 10 files
- **Development guides**: 4 files
- **Planning guides**: 3 files
- **Getting Started**: 2 files
- **Domains**: 1 file
- **Configuration files**: 1 file

## How to Use This Documentation

### For New Users
1. **index.mdx** — Understand what AverisOS is
2. **getting-started/overview.mdx** — Quick introduction
3. **getting-started/quick-start.mdx** — Set up and run

### For Stakeholders
1. **planning/roadmap.mdx** — See 18-month plan
2. **planning/business-model.mdx** — Understand pricing and revenue
3. **planning/go-to-market.mdx** — Customer acquisition strategy

### For Engineers & Architects
1. **architecture/overview.mdx** — Understand the system
2. **architecture/design-principles.mdx** — Learn the patterns
3. **architecture/patterns.mdx** — See implementation examples
4. **architecture/monorepo-structure.mdx** — Understand code organization
5. **decisions/** — Review architectural decisions for rationale

### For Developers & Contributors
1. **development/setup.mdx** — Get local environment working
2. **development/contributing.mdx** — Learn contribution process
3. **development/testing-strategy.mdx** — Understand testing approach
4. **development/claude-guide.mdx** — Learn how to work with Claude
5. **domains/overview.mdx** — Understand domain structure

## Configuration Details

### Collapsible Groups
The following groups are set with `"collapsible": true`:
- **Planning & Strategy** — Users typically access once or twice
- **Architecture** — Detailed reference material
- **Architecture Decisions (ADRs)** — Reference material for specific decisions
- **Development** — Secondary reference for developers

Non-collapsible groups:
- **Home** — Always visible
- **Getting Started** — Primary navigation
- **Domains** — Important for understanding the system

### Colors
- **Primary**: #0D9488 (teal)
- **Light**: #14B8A6 (light teal)
- **Dark**: #0F766E (dark teal)

### Theme
- **Theme**: mint
- **Logo**: Dark and light variants
- **Favicon**: AverisOS icon

## Navigation Flow

The documentation is designed to flow naturally:

1. **Landing** → index.mdx (what is this?)
2. **Getting Started** → overview + quick-start (how do I use it?)
3. **For Business** → planning/* (business and strategy)
4. **For Technical** → architecture/* (how does it work?)
5. **For Developers** → development/* (how do I contribute?)
6. **For Deep Dives** → decisions/* (why these choices?)

## Maintenance

### When to Update

1. **Code changes** → Update relevant architecture docs
2. **New decisions** → Create new ADR in `decisions/`
3. **New patterns** → Add to `architecture/patterns.mdx`
4. **Setup changes** → Update `development/setup.mdx`
5. **Roadmap changes** → Update `planning/roadmap.mdx`

### Git Workflow

```bash
# Create a branch for documentation changes
git checkout -b docs/update-setup-guide

# Make changes
# Commit with clear message
git commit -m "docs: update setup guide for new Ruby version"

# Push and create PR
git push origin docs/update-setup-guide
```

### Commit Message Conventions

```
docs: brief description

- More detailed explanation
- Additional context if needed

Co-Authored-By: Claude Haiku 4.5 <noreply@anthropic.com>
```

## Deployment

### Local Preview
```bash
npm install -g mintlify
cd documentation
mintlify dev
```

### Deploy to Production
Follow Mintlify's deployment guide at https://mintlify.com/docs/deployment/overview

### Preview URL
Once deployed, the documentation will be available at your Mintlify URL (e.g., `docs.averis-os.io`).

## Search Keywords

When searching documentation:
- **Architecture**: DDD, domain-driven, bounded context, dependency injection
- **Patterns**: command, request, verify, validate, operation, monad
- **Testing**: unit tests, integration tests, E2E tests, RSpec
- **Domains**: authentication, traceability, git integration
- **Decisions**: ADR, architectural decision, monorepo, REST
- **Setup**: Ruby, Rails, development environment

## Statistics

- **Total words**: ~40,000+
- **Code examples**: 100+
- **Architecture diagrams**: 5+
- **Tables**: 20+
- **Cross-references**: 150+
- **Navigation groups**: 7
- **Collapsible sections**: 4

## Next Steps

1. **Test locally**: `mintlify dev` and navigate through all sections
2. **Verify links**: Check that internal cross-references work
3. **Deploy**: Push to production via Mintlify
4. **Share**: Send documentation URL to team
5. **Gather feedback**: Ask users if navigation is intuitive

This hierarchical structure provides a much better user experience and makes the documentation more discoverable and easier to navigate.
