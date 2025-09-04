# PayloadCMS Configuration System

## Overview

The PayloadCMS configuration system provides a comprehensive and type-safe way to define the structure, behavior, and customization options for Payload applications. The configuration serves as the central blueprint that governs how Payload operates, from database connections and admin panel settings to collections, globals, and plugins.

## Architecture

### Core Configuration Files

The configuration system is built around several key modules:

- **`types.ts`** - Comprehensive TypeScript type definitions for all configuration options
- **`build.ts`** - Configuration building and plugin integration logic  
- **`sanitize.ts`** - Configuration validation and sanitization processes
- **`defaults.ts`** - Default configuration values and merging utilities
- **`find.ts`** - Configuration file discovery and resolution
- **`client.ts`** - Client-side configuration generation for admin panel
- **`orderable/`** - Support for orderable collections and documents

### Configuration Lifecycle

1. **Discovery**: Configuration files are located using `find.ts`
2. **Loading**: Raw configuration is imported and processed
3. **Plugin Integration**: Plugins modify configuration via `build.ts`
4. **Sanitization**: Configuration is validated and enhanced via `sanitize.ts`
5. **Client Generation**: Client-safe configuration is created via `client.ts`

## Core Configuration Types

### Main Configuration Interface

```typescript
export type Config = {
  // Database adapter configuration
  db: DatabaseAdapterResult
  
  // Application secret for encryption/signing
  secret: string
  
  // Collections configuration
  collections?: CollectionConfig[]
  
  // Global documents configuration
  globals?: GlobalConfig[]
  
  // Admin panel configuration
  admin?: AdminConfig
  
  // Plugin system
  plugins?: Plugin[]
  
  // Additional configuration options...
}
```

### Sanitized Configuration

The `SanitizedConfig` type represents the fully processed configuration after validation and enhancement:

```typescript
export type SanitizedConfig = {
  collections: SanitizedCollectionConfig[]
  globals: SanitizedGlobalConfig[]
  admin: DeepRequired<Config['admin']> & {
    timezones: SanitizedTimezoneConfig
  }
  // All properties are required and validated
}
```

## Key Features

### Plugin System

Plugins can modify configuration at build time:

```typescript
export type Plugin = (config: Config) => Config | Promise<Config>

// Example plugin usage
const myPlugin: Plugin = (config) => {
  config.collections?.push(myCustomCollection)
  return config
}
```

### Admin Panel Configuration

Comprehensive admin panel customization options:

```typescript
admin: {
  // User collection for authentication
  user?: string
  
  // Theme configuration
  theme?: 'all' | 'dark' | 'light'
  
  // Custom components
  components?: {
    beforeDashboard?: CustomComponent[]
    afterNavLinks?: CustomComponent[]
    // ... more component slots
  }
  
  // Routing configuration
  routes?: {
    admin?: string
    login?: string
    // ... other routes
  }
}
```

### Database Integration

Database adapters provide the persistence layer:

```typescript
db: DatabaseAdapterResult // Configured database adapter
```

### Localization Support

Multi-language content support:

```typescript
localization?: {
  locales: string[] | Locale[]
  defaultLocale: string
  fallback?: boolean
}
```

### Rich Text Editor Integration

Configurable rich text editing:

```typescript
editor?: RichTextAdapterProvider<any, any, any>
```

## Configuration Building Process

### Plugin Integration

The `buildConfig` function processes plugins sequentially:

```typescript
export async function buildConfig(config: Config): Promise<SanitizedConfig> {
  if (Array.isArray(config.plugins)) {
    let configAfterPlugins = config
    for (const plugin of config.plugins) {
      configAfterPlugins = await plugin(configAfterPlugins)
    }
    return await sanitizeConfig(configAfterPlugins)
  }
  return await sanitizeConfig(config)
}
```

### Configuration Sanitization

The sanitization process:

1. **Defaults Application**: Missing values are filled with defaults
2. **Validation**: Configuration is validated for correctness
3. **Enhancement**: Additional collections and features are added
4. **Relationship Resolution**: Inter-collection relationships are validated

### Client Configuration Generation

Server-only properties are filtered out for client use:

```typescript
export type ServerOnlyRootProperties = keyof Pick<
  SanitizedConfig,
  | 'db' | 'email' | 'hooks' | 'secret' 
  | 'plugins' | 'typescript' | 'cors' | 'csrf'
  // ... other server-only properties
>
```

## Advanced Features

### Orderable Collections

Automatic ordering support for collections and join fields:

```typescript
collection: {
  slug: 'posts',
  orderable: true, // Adds _order field and reorder endpoint
  fields: [
    // ... your fields
  ]
}
```

### Live Preview Configuration

Real-time preview of content changes:

```typescript
admin: {
  livePreview: {
    url: 'http://localhost:3000',
    breakpoints: [
      { name: 'mobile', width: 375, height: 667 }
    ]
  }
}
```

### Custom Endpoints

Add custom API endpoints:

```typescript
endpoints: [
  {
    path: '/custom-endpoint',
    method: 'get',
    handler: async (req) => {
      // Custom logic
      return new Response('Hello')
    }
  }
]
```

### Access Control

Granular permission system:

```typescript
access: {
  create: ({ req: { user } }) => !!user,
  read: () => true,
  update: ({ req: { user } }) => !!user,
  delete: ({ req: { user } }) => !!user?.role === 'admin'
}
```

## Configuration Discovery

### File Locations

Payload searches for configuration files in this order:

1. `PAYLOAD_CONFIG_PATH` environment variable location
2. TypeScript config-defined paths (`@payload-config`)
3. Standard locations: `src/`, project root, `dist/` (production)

### Supported Filenames

- `payload.config.ts` (development)
- `payload.config.js` (production/compiled)

## Default Configuration Values

Key defaults include:

```typescript
{
  defaultDepth: 2,
  maxDepth: 10,
  defaultMaxTextLength: 40000,
  cookiePrefix: 'payload',
  routes: {
    admin: '/admin',
    api: '/api',
    graphQL: '/graphql'
  },
  admin: {
    theme: 'all',
    dateFormat: 'MMMM do yyyy, h:mm a',
    avatar: 'gravatar'
  }
}
```

## Error Handling

The configuration system includes comprehensive error handling:

- **InvalidConfiguration**: Thrown for invalid configuration values
- **DuplicateCollection**: Thrown when collection slugs are duplicated
- **Missing Dependencies**: Validation of required dependencies

## Best Practices

### Type Safety

Always use TypeScript for configuration files to leverage full type checking:

```typescript
import type { Config } from 'payload/config'

export default {
  // Fully typed configuration
} satisfies Config
```

### Plugin Development

When creating plugins, ensure they're pure functions:

```typescript
export const myPlugin: Plugin = (config) => ({
  ...config,
  collections: [
    ...(config.collections || []),
    myNewCollection
  ]
})
```

### Performance Considerations

- Use `indexSortableFields` for better database performance
- Configure appropriate `defaultDepth` and `maxDepth` values
- Leverage client-side configuration filtering

## Integration Examples

### Basic Configuration

```typescript
import { buildConfig } from 'payload/config'

export default buildConfig({
  secret: process.env.PAYLOAD_SECRET!,
  db: mongooseAdapter({
    url: process.env.DATABASE_URI!,
  }),
  collections: [
    {
      slug: 'posts',
      fields: [
        { name: 'title', type: 'text', required: true },
        { name: 'content', type: 'richText' }
      ]
    }
  ]
})
```

### Advanced Configuration with Plugins

```typescript
import { buildConfig } from 'payload/config'
import { seoPlugin } from '@payloadcms/plugin-seo'
import { cloudStoragePlugin } from '@payloadcms/plugin-cloud-storage'

export default buildConfig({
  secret: process.env.PAYLOAD_SECRET!,
  db: mongooseAdapter({
    url: process.env.DATABASE_URI!,
  }),
  plugins: [
    seoPlugin({
      collections: ['posts', 'pages']
    }),
    cloudStoragePlugin({
      collections: {
        media: {
          adapter: s3Adapter({
            config: {
              region: process.env.S3_REGION,
              credentials: {
                accessKeyId: process.env.S3_ACCESS_KEY_ID!,
                secretAccessKey: process.env.S3_SECRET_ACCESS_KEY!,
              },
            },
            bucket: process.env.S3_BUCKET!,
          }),
        },
      },
    }),
  ],
  admin: {
    user: 'users',
    components: {
      beforeDashboard: ['@/components/CustomDashboard']
    }
  },
  collections: [
    // ... collection definitions
  ]
})
```

## Troubleshooting

### Common Issues

1. **Configuration Not Found**: Ensure configuration file is in expected location
2. **Type Errors**: Use proper TypeScript types for all configuration options
3. **Plugin Conflicts**: Check plugin order and compatibility
4. **Circular Dependencies**: Avoid circular references in collection relationships

### Debugging

Enable debug mode for detailed configuration information:

```typescript
debug: process.env.NODE_ENV !== 'production'
```

## Related Resources

- [Collections Configuration Documentation](../collections/collections-extended.md)
- [Global Configuration Documentation](../globals/globals-extended.md)
- [Admin Panel Configuration Documentation](../admin/admin-extended.md)
- [Field Configuration Documentation](../fields/fields-extended.md)