---
title: Vercel Postgres Database Adapter
label: Vercel Postgres
order: 10
desc: Vercel Postgres database adapter for PayloadCMS, enabling seamless integration with Vercel's managed PostgreSQL service
keywords: [vercel, postgres, database, adapter, payloadcms, sql, migration, drizzle]
---

<Banner type="warning">
**Original Documentation**: The content below comes from the original README.md file.
Further in the document, you'll find an extended, more detailed version of this documentation.
</Banner>

# Payload Postgres Adapter

[Vercel Postgres](https://vercel.com/docs/storage/vercel-postgres) adapter for [Payload](https://payloadcms.com).

- [Main Repository](https://github.com/payloadcms/payload)
- [Payload Docs](https://payloadcms.com/docs)

## Installation

```bash
npm install @payloadcms/db-vercel-postgres
```

## Usage

### Explicit Connection String

```ts
import { buildConfig } from 'payload'
import { vercelPostgresAdapter } from '@payloadcms/db-vercel-postgres'

export default buildConfig({
  db: vercelPostgresAdapter({
    pool: {
      connectionString: process.env.DATABASE_URI,
    },
  }),
  // ...rest of config
})
```

### Automatic Connection String Detection

Have Vercel automatically detect from environment variable (typically `process.env.POSTGRES_URL`)

```ts
export default buildConfig({
  db: postgresAdapter(),
  // ...rest of config
})
```

More detailed usage can be found in the [Payload Docs](https://payloadcms.com/docs/configuration/overview).

---

## 📚 Extended Documentation

<Banner type="success">
**Note**: The documentation below has been automatically generated based on source code analysis and contains more detailed information than the original documentation above.
</Banner>

![NPM Version](https://img.shields.io/npm/v/@payloadcms/db-vercel-postgres)
![Bundle Size](https://img.shields.io/bundlephobia/minzip/@payloadcms/db-vercel-postgres)

## Detailed Overview

The `@payloadcms/db-vercel-postgres` package is a specialized database adapter that connects PayloadCMS with Vercel Postgres, a fully managed PostgreSQL service. This adapter provides seamless integration between Payload's content management capabilities and Vercel's scalable database infrastructure.

**Key Benefits:**
- **Managed Infrastructure**: Leverages Vercel's fully managed PostgreSQL service
- **Automatic Scaling**: Built-in connection pooling and performance optimization
- **Local Development**: Smart detection of local vs. production environments
- **Migration Support**: Complete schema migration capabilities through Drizzle ORM
- **Type Safety**: Full TypeScript support with generated types

This adapter is designed for developers who want to deploy PayloadCMS applications on Vercel with minimal configuration while maintaining enterprise-grade database performance and reliability.

<Banner type="info">
The package is open-source. [View source code](https://github.com/payloadcms/payload/tree/main/packages/db-vercel-postgres). Need help? [Community Help](https://payloadcms.com/community-help).
</Banner>

## System Requirements

- **PayloadCMS**: 3.0.0 or higher
- **Node.js**: 18.0.0 or higher  
- **TypeScript**: 4.5.0 or higher (recommended)
- **Environment**: Vercel deployment or local development

## Installation

```bash
# npm
npm install @payloadcms/db-vercel-postgres

# yarn
yarn add @payloadcms/db-vercel-postgres

# pnpm
pnpm add @payloadcms/db-vercel-postgres
```

### Peer Dependencies

This package requires the following peer dependency:

```bash
# Payload CMS (automatically handled if using workspace)
npm install payload
```

**Core Dependencies Included:**
- `@vercel/postgres` (0.9.0) - Vercel Postgres client
- `drizzle-orm` (0.44.2) - TypeScript ORM
- `drizzle-kit` (0.31.4) - Database toolkit
- `pg` (8.16.3) - PostgreSQL client for local development

## Quick Start

Basic configuration with automatic environment detection:

```typescript
import { buildConfig } from 'payload'
import { vercelPostgresAdapter } from '@payloadcms/db-vercel-postgres'

export default buildConfig({
  // Automatic connection - uses POSTGRES_URL from Vercel
  db: vercelPostgresAdapter(),
  
  // Your collections, globals, etc.
  collections: [
    // your collections
  ],
})
```

### Environment Variables

```bash
# Required for Vercel deployment (automatically provided)
POSTGRES_URL=postgres://username:password@host:port/database

# Optional: Force Vercel Postgres even for localhost
FORCE_USE_VERCEL_POSTGRES=true

# Development: Drop database on restart (use with caution)
PAYLOAD_DROP_DATABASE=true
```

## Detailed Configuration

### Main Options

#### `pool`

- **Type**: `VercelPostgresPoolConfig`
- **Default value**: Uses Vercel environment variables
- **Required**: false

Configuration for the PostgreSQL connection pool. When not provided, Vercel Postgres automatically detects connection settings from environment variables.

```typescript
vercelPostgresAdapter({
  pool: {
    connectionString: process.env.POSTGRES_URL,
    // Additional pool options
    max: 20, // Maximum number of clients
    idleTimeoutMillis: 30000,
  },
})
```

#### `forceUseVercelPostgres`

- **Type**: `boolean`
- **Default value**: `false`
- **Required**: false

Forces the use of Vercel Postgres client even for local development. By default, the adapter uses the standard `pg` client for localhost connections.

```typescript
vercelPostgresAdapter({
  forceUseVercelPostgres: true, // Use Vercel client locally
})
```

#### `idType`

- **Type**: `'serial' | 'uuid'`
- **Default value**: `'serial'`
- **Required**: false

Determines the primary key type for database records. Serial uses auto-incrementing integers, while UUID uses universally unique identifiers.

```typescript
vercelPostgresAdapter({
  idType: 'uuid', // Use UUID instead of serial integers
})
```

#### `schemaName`

- **Type**: `string`
- **Default value**: `'public'`
- **Required**: false

**Experimental**: Specifies a custom database schema name. Currently has limitations with Drizzle when other tables exist with the same name in different schemas.

```typescript
vercelPostgresAdapter({
  schemaName: 'cms_data', // Use custom schema
})
```

#### `migrationDir`

- **Type**: `string`
- **Default value**: `'./migrations'`
- **Required**: false

Directory path for storing database migration files.

```typescript
vercelPostgresAdapter({
  migrationDir: './src/migrations',
})
```

#### `beforeSchemaInit` / `afterSchemaInit`

- **Type**: `PostgresSchemaHook[]`
- **Default value**: `[]`
- **Required**: false

Hooks for customizing the database schema before or after Payload's initialization.

```typescript
vercelPostgresAdapter({
  beforeSchemaInit: [
    ({ schema }) => {
      // Add custom tables or modify existing ones
      schema.customTable = pgTable('custom_table', {
        id: serial('id').primaryKey(),
        data: jsonb('data'),
      })
    }
  ],
  afterSchemaInit: [
    ({ schema }) => {
      // Additional customizations after Payload schema
    }
  ],
})
```

### Configuration Schema

```typescript
interface Args {
  // Connection and Pool Configuration
  pool?: VercelPostgresPoolConfig
  forceUseVercelPostgres?: boolean
  readReplicas?: string[]
  
  // Schema Configuration  
  idType?: 'serial' | 'uuid'
  schemaName?: string
  allowIDOnCreate?: boolean
  
  // Migration and Development
  migrationDir?: string
  disableCreateDatabase?: boolean
  push?: boolean
  prodMigrations?: Migration[]
  
  // Schema Hooks
  beforeSchemaInit?: PostgresSchemaHook[]
  afterSchemaInit?: PostgresSchemaHook[]
  
  // Advanced Options
  blocksAsJSON?: boolean
  extensions?: string[]
  localesSuffix?: string
  relationshipsSuffix?: string
  versionsSuffix?: string
  tablesFilter?: string[]
  transactionOptions?: false | PgTransactionConfig
  logger?: DrizzleConfig['logger']
}
```

## Usage Guides

### Basic Setup with Vercel

Deploy your PayloadCMS app to Vercel with these steps:

1. **Create Vercel Project**: Connect your GitHub repository to Vercel
2. **Add Postgres Storage**: In your Vercel dashboard, add Postgres storage
3. **Configure Adapter**: Use the basic configuration (environment variables are automatically set)

```typescript
// payload.config.ts
export default buildConfig({
  db: vercelPostgresAdapter(), // No configuration needed!
  // ... rest of your config
})
```

4. **Deploy**: Push to your connected branch to trigger deployment

### Local Development Setup

For local development, you have two options:

**Option 1: Local PostgreSQL Database**
```typescript
// Uses standard pg client for localhost
vercelPostgresAdapter({
  pool: {
    connectionString: 'postgres://user:pass@localhost:5432/mydb'
  }
})
```

**Option 2: Vercel Postgres with Docker**
```typescript
vercelPostgresAdapter({
  forceUseVercelPostgres: true,
  pool: {
    connectionString: process.env.POSTGRES_URL // From Vercel
  }
})
```

### Advanced Migration Management

```typescript
vercelPostgresAdapter({
  migrationDir: './database/migrations',
  prodMigrations: [
    {
      name: '20240101_initial_schema',
      up: async ({ sql }) => {
        await sql`CREATE INDEX idx_posts_status ON posts(status)`
      },
      down: async ({ sql }) => {
        await sql`DROP INDEX idx_posts_status`
      }
    }
  ]
})
```

### Read Replica Configuration

For high-traffic applications:

```typescript
vercelPostgresAdapter({
  readReplicas: [
    process.env.POSTGRES_READ_REPLICA_1_URL,
    process.env.POSTGRES_READ_REPLICA_2_URL,
  ]
})
```

## API Reference

### Functions

#### `vercelPostgresAdapter(args?: Args)`

Creates a Vercel Postgres database adapter instance.

**Parameters:**
| Parameter | Type | Description |
|-----------|------|-------------|
| `args` | `Args` | Configuration options (optional) |

**Returns:** `DatabaseAdapterObj<VercelPostgresAdapter>`

**Example:**
```typescript
const adapter = vercelPostgresAdapter({
  idType: 'uuid',
  pool: {
    connectionString: process.env.DATABASE_URL
  }
})
```

### TypeScript Types

```typescript
// Main adapter interface
export interface VercelPostgresAdapter extends BasePostgresAdapter {
  drizzle: NodePgDatabase
  pool?: VercelPool
  poolOptions?: Args['pool']
  forceUseVercelPostgres?: boolean
}

// Configuration arguments
export interface Args {
  pool?: VercelPostgresPoolConfig
  idType?: 'serial' | 'uuid'
  schemaName?: string
  migrationDir?: string
  beforeSchemaInit?: PostgresSchemaHook[]
  afterSchemaInit?: PostgresSchemaHook[]
  // ... additional options
}

// Migration types
export interface MigrateUpArgs {
  sql: ReturnType<typeof sql>
  payload: Payload
}

export interface MigrateDownArgs {
  sql: ReturnType<typeof sql>
  payload: Payload
}
```

## Integrations

### PayloadCMS Hooks

The adapter integrates with Payload's lifecycle hooks:

- **`beforeSchemaInit`**: Modify schema before Payload initialization
- **`afterSchemaInit`**: Add customizations after Payload schema creation
- **Connection lifecycle**: Automatic connection management and retry logic
- **Migration hooks**: Before/after migration execution hooks

### Database Integration

**Schema Management:**
- Automatic table creation for collections and globals  
- Version control tables (`_v` suffix)
- Relationship tables (`_rels` suffix)
- Localization tables (`_locales` suffix)

**Connection Pooling:**
- Intelligent local vs. production detection
- Automatic connection string resolution from Vercel environment
- Support for read replicas in high-traffic scenarios

### External Services

**Vercel Integration:**
- Seamless deployment with zero-configuration
- Automatic environment variable detection
- Built-in connection pooling and scaling

**Drizzle ORM:**
- Type-safe database operations
- Schema introspection and generation
- Migration management and version control

## Troubleshooting

### Common Issues

#### Connection Refused in Local Development

**Problem:** Getting "Connection refused" or "ECONNREFUSED" errors locally

**Solution:**
Ensure your local PostgreSQL is running, or use Docker:

```bash
# Using Docker
docker run --name postgres-dev -e POSTGRES_PASSWORD=mypassword -d -p 5432:5432 postgres

# Update your .env
POSTGRES_URL=postgres://postgres:mypassword@localhost:5432/mydatabase
```

#### Migration Lock Issues

**Problem:** "Migration lock" or "Migration already in progress" errors

**Solution:**
Clear the migration lock manually:

```typescript
// In your migration script
await sql`DELETE FROM drizzle.__drizzle_migrations WHERE success = false`
```

#### Schema Conflicts

**Problem:** Tables already exist errors during initialization

**Solution:**
Use the drop database flag for development (CAUTION: destroys data):

```bash
PAYLOAD_DROP_DATABASE=true npm run dev
```

#### Type Generation Issues

**Problem:** Generated types are outdated or missing

**Solution:**
Regenerate your payload types:

```bash
npx payload generate:types
```

### Debugging

Enable detailed logging for troubleshooting:

```typescript
vercelPostgresAdapter({
  logger: {
    logQuery: (query, params) => {
      console.log('SQL:', query)
      console.log('Params:', params)
    },
  },
})
```

For connection debugging, check environment variables:

```typescript
// Add to your config
console.log('Database URL:', process.env.POSTGRES_URL?.replace(/:[^:]*@/, ':***@'))
```

## Migration

### Schema Changes

When making changes to your collections or fields:

1. **Development**: Changes are automatically applied via `push: true`
2. **Production**: Generate and run migrations:

```bash
# Generate migration
npx payload migrate:create

# Run migrations in production
npx payload migrate
```

### Version Compatibility

The adapter follows Payload's versioning. For major version updates:

- Review the [CHANGELOG](https://github.com/payloadcms/payload/tree/main/packages/db-vercel-postgres) 
- Test migrations in a staging environment
- Update your `payload.config.ts` configuration as needed

## Performance

### Connection Optimization

```typescript
vercelPostgresAdapter({
  pool: {
    max: 20,                    // Max connections
    idleTimeoutMillis: 30000,   // Close idle connections
    connectionTimeoutMillis: 2000, // Connection timeout
  }
})
```

### Query Performance

- **Indexes**: Use `afterSchemaInit` hooks to add custom indexes
- **Read Replicas**: Configure for read-heavy workloads
- **Connection Pooling**: Enabled by default via Vercel Postgres

## Security

### Best Practices

- **Never expose database URLs**: Use environment variables
- **Connection Limits**: Configure appropriate pool sizes  
- **Schema Isolation**: Consider using custom schema names for multi-tenant apps
- **Migration Safety**: Always backup before running migrations in production

### Environment Security

```typescript
// Good: Environment variables
vercelPostgresAdapter({
  pool: {
    connectionString: process.env.POSTGRES_URL
  }
})

// Bad: Hardcoded credentials
vercelPostgresAdapter({
  pool: {
    connectionString: 'postgres://user:password@host/db' // Never do this
  }
})
```

## Example Projects

- [Vercel Postgres Template](https://github.com/payloadcms/payload/tree/main/templates/with-vercel-postgres) - Complete starter template
- [E-commerce Example](https://github.com/payloadcms/payload/tree/main/examples/ecommerce) - Advanced usage with custom schema hooks

## Contributing

Found a bug or have a suggestion? [Open an issue](https://github.com/payloadcms/payload/issues) or submit a Pull Request.

## License

MIT License - see the [LICENSE](https://github.com/payloadcms/payload/blob/main/packages/db-vercel-postgres/license.md) file for details.