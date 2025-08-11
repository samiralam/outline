# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Build and Development Commands

```bash
# Build the entire application
yarn build

# Start development server (separate backend/frontend)
yarn dev:watch

# Development with only backend changes
yarn dev:backend

# Development with only frontend changes  
yarn vite:dev

# Production start
yarn start

# Database operations
yarn db:migrate
yarn db:create-migration
yarn db:reset
```

## Testing

```bash
# Run all tests
yarn test

# Run specific test suites
yarn test:server      # Backend tests only
yarn test:app         # Frontend tests only
yarn test:shared      # Shared code tests

# Run single test file
yarn test:server myTestFile
```

## Linting and Formatting

```bash
# Lint all code
yarn lint

# Lint only changed files
yarn lint:changed

# Format code
yarn format

# Check formatting
yarn format:check
```

## Architecture Overview

Outline is a TypeScript monorepo with three main sections:

### Frontend (`/app`)
- **Framework**: React with Vite build system
- **State**: MobX for state management
- **Styling**: Styled Components
- **Key directories**:
  - `components/` - Reusable React components
  - `scenes/` - Full-page views
  - `stores/` - MobX stores for state management
  - `models/` - Frontend data models
  - `hooks/` - Custom React hooks

### Backend (`/server`) 
- **Framework**: Koa.js API server
- **Database**: PostgreSQL with Sequelize ORM
- **Background Jobs**: Redis with Bull queues
- **Authorization**: cancan-based policies
- **Key directories**:
  - `models/` - Sequelize database models
  - `policies/` - Authorization logic
  - `commands/` - Complex multi-model operations
  - `presenters/` - API response formatting
  - `migrations/` - Database schema changes

### Shared (`/shared`)
- Common code used by both frontend and backend
- Editor logic based on ProseMirror
- Shared utilities and components
- TypeScript types and validation schemas

## Path Aliases

The codebase uses these import aliases:
- `@server/*` → `./server/*`
- `@shared/*` → `./shared/*` 
- `~/*` → `./app/*`

## Database

- Uses PostgreSQL with Sequelize ORM
- Migrations in `server/migrations/`
- All models support soft deletion (paranoid mode)
- Full-text search capabilities built-in

## Key Technologies

- **Frontend**: React 17, MobX 4, Styled Components, Vite
- **Backend**: Koa, Sequelize, PostgreSQL, Redis, Bull
- **Editor**: ProseMirror-based collaborative editor
- **Real-time**: Socket.io for websockets
- **Background Jobs**: Bull queues with Redis
- **Authentication**: Passport.js with multiple providers
- **File Storage**: S3-compatible storage

## Development Notes

- All code is TypeScript with strict settings
- Jest is used for testing with separate configs for app/server/shared
- ESLint (oxlint) and Prettier are enforced
- The app uses collaborative editing with real-time synchronization
- Background job processing handles async operations like imports/exports
- Plugin system supports external integrations