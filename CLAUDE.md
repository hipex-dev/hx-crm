# HX-CRM - HIPEX Customer Relationship Management

## Project Overview

**HX-CRM** is HIPEX's customized fork of [Twenty](https://github.com/twentyhq/twenty), the #1 open-source CRM and a modern, community-powered alternative to Salesforce.

### Project Details

- **Status**: 🚧 In Development
- **Type**: Web Application (Fork/Customization)
- **Original Source**: [Twenty](https://github.com/twentyhq/twenty)
- **Technology Stack**:
  - Frontend: React 18, Recoil, Emotion, Vite
  - Backend: NestJS, TypeORM, BullMQ, GraphQL
  - Database: PostgreSQL, Redis, ClickHouse (analytics)
  - Language: TypeScript (98.8%)
  - Build System: Nx (monorepo)
  - Package Manager: Yarn 4

### Repository Structure

- **Origin**: `https://github.com/hipex-dev/hx-crm.git` (HIPEX fork)
- **Upstream**: `https://github.com/twentyhq/twenty.git` (Original Twenty)

---

## HIPEX Customization Guide

### Purpose

This fork allows HIPEX to:
- Customize Twenty CRM for internal customer relationship management
- Add HIPEX-specific features and integrations
- Maintain control over deployment and updates
- Contribute improvements back to upstream when applicable
- Build a comprehensive CRM solution tailored to HIPEX workflows

### Syncing with Upstream

To pull updates from the original Twenty repository:

```bash
# Fetch upstream changes
git fetch upstream

# Merge upstream changes into main branch
git checkout main
git merge upstream/main

# Resolve any conflicts if needed
# Push updates to HIPEX fork
git push origin main
```

### Customization Strategy

1. **Maintain Upstream Compatibility**: Keep core Twenty functionality intact
2. **HIPEX Extensions**: Add custom features in separate modules/components
3. **Documentation**: Document all customizations in this file
4. **Testing**: Test thoroughly before deploying HIPEX-specific changes
5. **License Compliance**: Respect AGPL-3.0 license requirements

### HIPEX-Specific Features

#### Planned Customizations
- [ ] HIPEX branding and theming
- [ ] Integration with HIPEX authentication system (SSO)
- [ ] Custom fields for HIPEX business processes
- [ ] Enhanced workflow automation for HIPEX operations
- [ ] Integration with other HIPEX tools (hx-kanban, hx-wiki)
- [ ] Custom reporting and analytics dashboards
- [ ] HIPEX-specific data import/export tools
- [ ] VPS deployment com Docker Swarm (parte do hipex-stack)

#### Implemented Features
(None yet - project just forked on 2025-10-12)

**Next Phase**: Setup ambiente de desenvolvimento local após conclusão da migração VPS (ver `/MIGRATION-PLAN.md`)

---

## Development Environment

### Key Commands

#### Development
```bash
# Start full development environment (frontend + backend + worker)
yarn start

# Individual package development
npx nx start twenty-front         # Start frontend dev server
npx nx start twenty-server        # Start backend server
npx nx run twenty-server:worker   # Start background worker
```

#### Testing
```bash
# Unit tests
npx nx test twenty-front          # Frontend unit tests
npx nx test twenty-server         # Backend unit tests

# Integration tests
npx nx run twenty-server:test:integration:with-db-reset

# Storybook
npx nx storybook:build twenty-front
npx nx storybook:serve-and-test:static twenty-front
```

#### Code Quality
```bash
# Linting
npx nx lint twenty-front          # Frontend linting
npx nx lint twenty-server         # Backend linting
npx nx lint twenty-front --fix    # Auto-fix linting issues

# Type checking
npx nx typecheck twenty-front
npx nx typecheck twenty-server

# Format code
npx nx fmt twenty-front
npx nx fmt twenty-server
```

#### Build
```bash
# Build packages
npx nx build twenty-front
npx nx build twenty-server
```

#### Database Operations
```bash
# Database management
npx nx database:reset twenty-server              # Reset database
npx nx run twenty-server:database:init:prod      # Initialize database
npx nx run twenty-server:database:migrate:prod   # Run migrations

# Generate migration
npx nx run twenty-server:typeorm migration:generate src/database/typeorm/core/migrations/[name] -d src/database/typeorm/core/core.datasource.ts

# Sync metadata
npx nx run twenty-server:command workspace:sync-metadata -f
```

#### GraphQL
```bash
# Generate GraphQL types
npx nx run twenty-front:graphql:generate
```

---

## Architecture Overview

### Tech Stack Details
- **Frontend**: React 18, TypeScript, Recoil (state management), Emotion (styling), Vite
- **Backend**: NestJS, TypeORM, PostgreSQL, Redis, GraphQL (with GraphQL Yoga)
- **Monorepo**: Nx workspace managed with Yarn 4

### Package Structure
```
packages/
├── twenty-front/          # React frontend application
├── twenty-server/         # NestJS backend API
├── twenty-ui/             # Shared UI components library
├── twenty-shared/         # Common types and utilities
├── twenty-emails/         # Email templates with React Email
├── twenty-website/        # Next.js documentation website
├── twenty-zapier/         # Zapier integration
└── twenty-e2e-testing/    # Playwright E2E tests
```

### Key Development Principles
- **Functional components only** (no class components)
- **Named exports only** (no default exports)
- **Types over interfaces** (except when extending third-party interfaces)
- **String literals over enums** (except for GraphQL enums)
- **No 'any' type allowed**
- **Event handlers preferred over useEffect** for state updates

### State Management
- **Recoil** for global state management
- Component-specific state with React hooks
- GraphQL cache managed by Apollo Client

### Backend Architecture
- **NestJS modules** for feature organization
- **TypeORM** for database ORM with PostgreSQL
- **GraphQL** API with code-first approach
- **Redis** for caching and session management
- **BullMQ** for background job processing

### Database
- **PostgreSQL** as primary database
- **Redis** for caching and sessions
- **TypeORM migrations** for schema management
- **ClickHouse** for analytics (when enabled)

---

## HIPEX Development Workflow

### Before Making Changes
1. Always run linting and type checking after code changes
2. Test changes with relevant test suites
3. Ensure database migrations are properly structured
4. Check that GraphQL schema changes are backward compatible
5. Document HIPEX customizations in this file
6. Follow HIPEX development standards from workspace `CLAUDE.md`

### Code Style Notes
- Use **Emotion** for styling with styled-components pattern
- Follow **Nx** workspace conventions for imports
- Use **Lingui** for internationalization
- Components should be in their own directories with tests and stories

### Testing Strategy
- **Unit tests** with Jest for both frontend and backend
- **Integration tests** for critical backend workflows
- **Storybook** for component development and testing
- **E2E tests** with Playwright for critical user flows

---

## Resources

- [Twenty Official Website](https://twenty.com)
- [Twenty Documentation](https://twenty.com/developers)
- [Twenty GitHub Repository](https://github.com/twentyhq/twenty)
- [Twenty Community Discord](https://twenty.com/discord)
- Original README: See `README.md` in this directory

---

## License & Compliance

**Important**: Twenty CRM uses a dual-license model:
- **AGPL-3.0**: For open-source use
- **Commercial License**: Available for enterprise features marked with `/* @license Enterprise */`

HIPEX's fork must comply with AGPL-3.0 requirements:
- Source code must remain open if distributed
- Modifications must be shared under AGPL-3.0
- Network use (SaaS) requires source availability

For commercial features or closed-source deployment, contact Twenty for commercial licensing options.

---

## Notes

- **Fork Created**: 2025-10-12
- **Original Version**: Latest from Twenty main branch at fork time
- **Upstream Stars**: 35,800+ (highly active community)
- **Upstream Contributors**: 522+
- **Upstream Forks**: 4,300+
- **Maintenance**: Regularly sync with upstream for security updates and improvements
- **Deployment**: Self-hosted on HIPEX infrastructure (configuration TBD)
- **VPS Migration**: Planejamento completo disponível em `/MIGRATION-PLAN.md` - arquitetura hipex-stack projetada para deployment em VPS Contabo 400 GB NVMe com 12 vCores, 48GB RAM

## Important Files
- `nx.json` - Nx workspace configuration with task definitions
- `tsconfig.base.json` - Base TypeScript configuration
- `package.json` - Root package with workspace definitions
- `.cursor/rules/` - Development guidelines and best practices (from upstream)
