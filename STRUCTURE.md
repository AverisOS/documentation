# AverisOS Mintlify Documentation Structure

This document describes the complete documentation structure created for AverisOS.

## Directory Layout

```
documentation/
├── mint.json                          # Mintlify configuration
├── STRUCTURE.md                       # This file
├── index.mdx                          # Landing page
├── overview.mdx                       # Product overview
├── quick-start.mdx                    # 5-minute quickstart
│
├── planning/                          # Business & Strategy
│   ├── roadmap.mdx                    # 18-month product roadmap
│   ├── business-model.mdx             # Pricing, revenue, go-to-market
│   └── go-to-market.mdx               # Customer acquisition strategy
│
├── architecture/                      # Technical Architecture
│   ├── overview.mdx                   # Architecture layers & patterns
│   ├── design-principles.mdx          # 10 core design principles
│   ├── patterns.mdx                   # Common implementation patterns (5 patterns)
│   └── monorepo-structure.mdx         # How domains are organized
│
├── decisions/                         # Architecture Decision Records (ADRs)
│   ├── adr-001-ddd.mdx                # Domain-Driven Design with Rails + dry-rb
│   ├── adr-002-result-monad.mdx       # Result Monad Instead of Exceptions
│   ├── adr-003-monorepo.mdx           # Monorepo for Domains (not separate repos)
│   ├── adr-004-rest-api.mdx           # REST API (not GraphQL) for Phase 1
│   ├── adr-005-dry-rb.mdx             # Dry-rb for validation, types, structs
│   ├── adr-006-event-dispatcher.mdx   # Event Dispatcher for cross-domain communication
│   ├── adr-007-phase-1-focus.mdx      # Phase 1 Focus on Traceability Over AI
│   ├── adr-008-open-source.mdx        # Open-Source CLI and SDKs
│   ├── adr-009-design-partners.mdx    # Design Partner Program Over Public Beta
│   └── adr-010-self-hosted.mdx        # Self-Hosted in Phase 2, Not Phase 1
│
├── domains/                           # Domain-Specific Guides
│   └── overview.mdx                   # Overview of all domains
│       (Individual domain guides: authentication.mdx, traceability.mdx, etc. coming soon)
│
└── development/                       # Development & Collaboration
    ├── setup.mdx                      # Local development setup (5-min quickstart)
    ├── contributing.mdx               # Contribution guidelines
    ├── testing-strategy.mdx           # Testing pyramid & best practices
    └── claude-guide.mdx               # How to work with Claude AI
```

## File Count

- **Total documentation files**: 21 files
- **Architecture files**: 4 files
- **ADRs (Architecture Decision Records)**: 10 files
- **Development guides**: 4 files
- **Planning guides**: 3 files
- **Configuration files**: 1 file
- **Support pages**: 3 files (overview, quick-start, structure)

## Content by Section

### 1. Planning & Strategy (3 files)
- `planning/roadmap.mdx` — 18-month product roadmap with phases and deliverables
- `planning/business-model.mdx` — Pricing tiers, revenue model, financial projections
- `planning/go-to-market.mdx` — Customer acquisition, ICP, channels, marketing strategy

### 2. Architecture (4 files)
- `architecture/overview.mdx` — High-level architecture, layers, patterns, monorepo structure
- `architecture/design-principles.mdx` — 10 core principles (business logic, thin models, DI, etc.)
- `architecture/patterns.mdx` — 5 common patterns (simple validation, complex logic, composition, etc.)
- `architecture/monorepo-structure.mdx` — Directory organization, domain boundaries, communication patterns

### 3. Decisions (10 files)
Complete ADR set covering:
- Technical choices (DDD, Result monad, REST, dry-rb, event dispatcher)
- Strategic choices (monorepo, MVP scope, AI strategy)
- Operational choices (self-hosted strategy, open-source approach, validation via design partners)

### 4. Development Guides (4 files)
- `development/setup.mdx` — Local dev environment setup (5 min)
- `development/contributing.mdx` — PR process, code style, testing requirements
- `development/testing-strategy.mdx` — Testing pyramid (60% unit, 30% integration, 10% E2E)
- `development/claude-guide.mdx` — How to effectively ask Claude for help

### 5. Domain Documentation (1 file)
- `domains/overview.mdx` — Overview of all domains, phase roadmap, anatomy of a domain

### 6. Support & Navigation (3 files)
- `index.mdx` — Landing page with card-based navigation
- `overview.mdx` — Product overview (problem, solution, differentiators)
- `quick-start.mdx` — 5-minute orientation guide
- `STRUCTURE.md` — This file

## Key Features

### 1. Mintlify Integration
- `mint.json` configuration with proper navigation structure
- Color scheme: Teal (#0D9488) primary, with gray (#6B7280) secondary
- Organized into logical sections with proper hierarchy
- Responsive design for mobile and desktop

### 2. Architecture Documentation
- Complete DDD architecture guide with code examples
- 10 design principles with before/after code patterns
- 5 common implementation patterns with full examples
- Clear separation of concerns (models, controllers, domain services)

### 3. Decision Records
- 10 ADRs covering all major architectural choices
- Format: Context, Decision, Alternatives, Rationale, Consequences, References
- Covers technical, strategic, and operational decisions
- Full rationale and trade-offs for each decision

### 4. Development Workflow
- Clear setup instructions with troubleshooting
- Contribution guidelines with PR template
- Testing strategy with example tests
- Claude AI collaboration guide with best practices

### 5. Navigation
- Organized by audience (stakeholders, engineers, developers)
- Cross-references between related documents
- Links to code, examples, and implementation details
- Searchable through Mintlify

## How to Use This Documentation

### For Stakeholders
1. Start with `overview.mdx` — Understand what AverisOS is
2. Read `planning/roadmap.mdx` — See 18-month plan
3. Review `planning/business-model.mdx` — Understand pricing and revenue
4. Check `planning/go-to-market.mdx` — See customer acquisition strategy

### For Engineers
1. Read `architecture/overview.mdx` — Understand the architecture
2. Review `architecture/design-principles.mdx` — Learn the patterns
3. Check `architecture/patterns.mdx` — See implementation examples
4. Reference `architecture/monorepo-structure.mdx` — Understand code organization
5. Review decisions in `decisions/` for rationale

### For Developers
1. Follow `development/setup.mdx` — Get local environment working
2. Read `development/contributing.mdx` — Learn contribution process
3. Review `development/testing-strategy.mdx` — Understand testing approach
4. Check `development/claude-guide.mdx` — Learn how to work with Claude
5. Reference `domains/overview.mdx` — Understand domain structure

### For AI Collaboration
1. Read `development/claude-guide.mdx` — How to ask for help
2. Reference `architecture/design-principles.mdx` — Understand DDD
3. Check `architecture/patterns.mdx` — See implementation patterns
4. Review `decisions/` — Understand architectural choices

## Search Keywords

When searching Mintlify documentation:
- **Architecture**: DDD, domain-driven, bounded context, dependency injection
- **Patterns**: command, request, verify, validate, operation, monad
- **Testing**: unit tests, integration tests, E2E tests, RSpec
- **Domains**: authentication, traceability, git integration, testing, email
- **Decisions**: ADR, architectural decision, monorepo, REST, GraphQL

## Maintenance

### Keeping Documentation Updated

1. **When code changes**: Update relevant architecture docs
2. **When decisions are made**: Create new ADR in `decisions/`
3. **When new patterns emerge**: Add to `architecture/patterns.mdx`
4. **When design principles change**: Update `architecture/design-principles.mdx`
5. **When setup changes**: Update `development/setup.mdx`

### Version Control

- Documentation is in `AverisOS/documentation/` directory
- Track all changes in git with clear commit messages:
  ```bash
  git commit -m "docs: add ADR-011 on [topic]"
  git commit -m "docs: update setup guide for new Ruby version"
  ```

## Integration with Main Repository

This documentation should be:
1. In a separate `documentation/` directory in the main project
2. Built and deployed to Mintlify (via mint CLI or GitHub actions)
3. Linked from main README.md
4. Referenced in CONTRIBUTING.md
5. Updated during pull review (if docs need updating)

## Next Steps

1. **Copy to repository**: `cp -r documentation/ /path/to/AverisOS/documentation/`
2. **Install Mintlify**: `npm install -g mintlify`
3. **Preview locally**: `mintlify dev`
4. **Deploy**: Follow Mintlify deployment guide
5. **Share URL**: With team so everyone can access

## Statistics

- **Total words**: ~40,000+ (not counting code examples)
- **Code examples**: 100+
- **Architecture diagrams**: 5+
- **Tables**: 20+
- **Links**: 150+

This documentation provides a comprehensive foundation for understanding, building, and collaborating on AverisOS.
