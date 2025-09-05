---
title: Locked Documents Core Module
label: Locked Documents
order: 40
desc: Internal PayloadCMS module providing document locking infrastructure, collection configuration, and concurrency control for collaborative editing.
keywords: [locked, documents, locking, concurrency, editing, collection, collaboration, payload, admin, database]
---

<Banner type="warning">
**Original Documentation**: The content below comes from [official PayloadCMS documentation](../../../docs/admin/locked-documents.mdx).
Further in the document, you'll find an extended, more detailed version of this documentation.
</Banner>

Document locking in Payload ensures that only one user at a time can edit a document, preventing data conflicts and accidental overwrites. When a document is locked, other users are prevented from making changes until the lock is released, ensuring data integrity in collaborative environments.

The lock is automatically triggered when a user begins editing a document within the Admin Panel and remains in place until the user exits the editing view or the lock expires due to inactivity.

## How it works

When a user starts editing a document, Payload locks it for that user. If another user attempts to access the same document, they will be notified that it is currently being edited. They can then choose one of the following options:

- View in Read-Only: View the document without the ability to make any changes.
- Take Over: Take over editing from the current user, which locks the document for the new editor and notifies the original user.
- Return to Dashboard: Navigate away from the locked document and continue with other tasks.

The lock will automatically expire after a set period of inactivity, configurable using the `duration` property in the `lockDocuments` configuration, after which others can resume editing.

<Banner type="info">
  **Note:** If your application does not require document locking, you can
  disable this feature for any collection or global by setting the
  `lockDocuments` property to `false`.
</Banner>

### Config Options

The `lockDocuments` property exists on both the Collection Config and the Global Config. Document locking is enabled by default, but you can customize the lock duration or turn off the feature for any collection or global.

Here's an example configuration for document locking:

```ts
import type { CollectionConfig } from 'payload'

export const Posts: CollectionConfig = {
  slug: 'posts',
  fields: [
    {
      name: 'title',
      type: 'text',
    },
    // other fields...
  ],
  lockDocuments: {
    duration: 600, // Duration in seconds
  },
}
```

#### Locking Options

| Option              | Description                                                                                                                                                                    |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **`lockDocuments`** | Enables or disables document locking for the collection or global. By default, document locking is enabled. Set to an object to configure, or set to false to disable locking. |
| **`duration`**      | Specifies the duration (in seconds) for how long a document remains locked without user interaction. The default is 300 seconds (5 minutes).                                   |

### Impact on APIs

Document locking affects both the Local and REST APIs, ensuring that if a document is locked, concurrent users will not be able to perform updates or deletes on that document (including globals). If a user attempts to update or delete a locked document, they will receive an error.

Once the document is unlocked or the lock duration has expired, other users can proceed with updates or deletes as normal.

#### Overriding Locks

For operations like `update` and `delete`, Payload includes an `overrideLock` option. This boolean flag, when set to `false`, enforces document locks, ensuring that the operation will not proceed if another user currently holds the lock.

By default, `overrideLock` is set to `true`, which means that document locks are ignored, and the operation will proceed even if the document is locked. To enforce locks and prevent updates or deletes on locked documents, set `overrideLock: false`.

```ts
const result = await payload.update({
  collection: 'posts',
  id: '123',
  data: {
    title: 'New title',
  },
  overrideLock: false, // Enforces the document lock, preventing updates if the document is locked
})
```

This option is particularly useful in scenarios where administrative privileges or specific workflows require you to override the lock and ensure the operation is completed.

---

## 📚 Extended Documentation

<Banner type="success">
**Note**: The documentation below has been automatically generated based on source code analysis and contains more detailed information than the original documentation above.
</Banner>

## Detailed Overview

The PayloadCMS Locked Documents Core Module provides the foundational infrastructure for document locking functionality within PayloadCMS. This internal system ensures data integrity and prevents concurrent editing conflicts by managing document locks across collections and globals, maintaining user sessions, and providing automatic cleanup of expired locks.

The module creates and manages a special internal collection called `payload-locked-documents` that tracks which documents are currently being edited, by whom, and when the lock should expire. This system is seamlessly integrated into PayloadCMS's CRUD operations and provides both programmatic and admin interface protection against concurrent modifications.

Key benefits include prevention of data loss from concurrent edits, automatic lock expiration to prevent permanent locks, support for both collections and globals, user-friendly admin interface notifications, and programmatic API access control with configurable override options.

<Banner type="info">
The package is open-source. [View source code](https://github.com/payloadcms/payload/tree/main/packages/payload/src/locked-documents). Need help? [Community Help](https://payloadcms.com/community-help).
</Banner>

## System Requirements

- **PayloadCMS**: ^3.0.0
- **Node.js**: >=18.0.0
- **Database**: MongoDB, PostgreSQL, or SQLite
- **Authentication**: Requires at least one authenticated collection

## Installation

The locked documents module is included automatically with PayloadCMS core and doesn't require separate installation:

```bash
# npm
npm install payload

# yarn  
yarn add payload

# pnpm
pnpm add payload
```

## Quick Start

Document locking is enabled by default. Configure it in your collection or global configuration:

```typescript
import type { CollectionConfig } from 'payload'

export const Posts: CollectionConfig = {
  slug: 'posts',
  // Default: locking enabled with 5-minute duration
  lockDocuments: {
    duration: 600 // 10 minutes in seconds
  },
  fields: [
    {
      name: 'title',
      type: 'text',
    },
  ]
}
```

### Disable locking for specific collections

```typescript
export const PublicPosts: CollectionConfig = {
  slug: 'public-posts',
  lockDocuments: false, // Disable locking completely
  fields: [
    // ... your fields
  ]
}
```

## Detailed Configuration

### Main Options

#### `lockDocuments`

- **Type**: `{ duration: number } | false`
- **Default**: `{ duration: 300 }` (5 minutes)
- **Required**: No

Controls document locking behavior for the collection or global. When set to an object, enables locking with specified duration. When set to `false`, disables locking entirely.

```typescript
// Enable with custom duration
lockDocuments: {
  duration: 900 // 15 minutes
}

// Disable locking
lockDocuments: false
```

#### `duration`

- **Type**: `number`
- **Default**: `300` (5 minutes)
- **Required**: No (when lockDocuments is an object)

Specifies how long (in seconds) a document remains locked without user interaction before the lock expires automatically.

```typescript
lockDocuments: {
  duration: 1800 // 30 minutes = 1800 seconds
}
```

### Configuration Schema

```typescript
// Collection configuration type
interface CollectionConfig {
  lockDocuments?: {
    duration: number
  } | false
  // ... other collection options
}

// Global configuration type  
interface GlobalConfig {
  lockDocuments?: {
    duration: number
  } | false
  // ... other global options
}

// Internal locked document structure
interface LockedDocument {
  id: string
  document: {
    relationTo: string
    value: string | number
  }
  globalSlug?: string
  user: {
    relationTo: string
    value: string | number  
  }
  createdAt: string
  updatedAt: string
}
```

## Usage Guides

### Configuring Collection-Level Locking

Set up document locking for different collections based on their collaboration needs:

```typescript
import type { CollectionConfig } from 'payload'

// High-collaboration collection with shorter lock duration
export const Articles: CollectionConfig = {
  slug: 'articles',
  lockDocuments: {
    duration: 180 // 3 minutes for quick turnaround
  },
  fields: [
    { name: 'title', type: 'text' },
    { name: 'content', type: 'richText' },
  ]
}

// Administrative collection with longer lock duration
export const Settings: CollectionConfig = {
  slug: 'settings', 
  lockDocuments: {
    duration: 1800 // 30 minutes for careful editing
  },
  fields: [
    { name: 'siteName', type: 'text' },
    { name: 'config', type: 'json' },
  ]
}

// Public collection with no locking needed
export const Categories: CollectionConfig = {
  slug: 'categories',
  lockDocuments: false, // No locking for simple data
  fields: [
    { name: 'name', type: 'text' },
  ]
}
```

### Working with Globals Locking

Configure document locking for global documents that require careful coordination:

```typescript
import type { GlobalConfig } from 'payload'

export const SiteSettings: GlobalConfig = {
  slug: 'site-settings',
  lockDocuments: {
    duration: 900 // 15 minutes for site-wide changes
  },
  fields: [
    { name: 'maintenanceMode', type: 'checkbox' },
    { name: 'announcements', type: 'array', fields: [...] },
  ]
}

export const Navigation: GlobalConfig = {
  slug: 'navigation',
  lockDocuments: {
    duration: 600 // 10 minutes for menu changes
  },
  fields: [
    { name: 'items', type: 'array', fields: [...] },
  ]
}
```

### Advanced Patterns

#### Programmatic Lock Override

Use the `overrideLock` option in your operations to bypass lock protection when necessary:

```typescript
import type { Payload } from 'payload'

// Administrative override function
async function emergencyUpdateDocument(payload: Payload, id: string, data: any) {
  try {
    // Attempt normal update (respects locks)
    const result = await payload.update({
      collection: 'posts',
      id,
      data,
      overrideLock: false // Enforce lock protection
    })
    return result
  } catch (error) {
    if (error.name === 'Locked') {
      console.warn(`Document ${id} is locked, forcing update...`)
      
      // Administrative override (bypasses locks)
      return await payload.update({
        collection: 'posts', 
        id,
        data,
        overrideLock: true // Force update despite lock
      })
    }
    throw error
  }
}
```

#### Custom Lock Status Checking

Create utility functions to check document lock status before attempting operations:

```typescript
import { checkDocumentLockStatus } from 'payload'
import type { PayloadRequest } from 'payload'

async function safeDocumentUpdate(req: PayloadRequest, collectionSlug: string, id: string, data: any) {
  try {
    // Check lock status first
    await checkDocumentLockStatus({
      req,
      collectionSlug,
      id,
      overrideLock: false, // Enforce lock checking
      lockErrorMessage: `Cannot update ${collectionSlug} ${id}: document is being edited by another user`
    })
    
    // Proceed with update if not locked
    return await req.payload.update({
      collection: collectionSlug,
      id,
      data,
      overrideLock: false
    })
  } catch (error) {
    if (error.name === 'Locked') {
      // Handle locked document gracefully
      return {
        success: false,
        error: 'Document is currently locked',
        message: error.message
      }
    }
    throw error
  }
}
```

## API Reference

### Constants

#### `lockedDocumentsCollectionSlug`

- **Value**: `'payload-locked-documents'`
- **Description**: The slug of the internal collection used to track locked documents

```typescript
import { lockedDocumentsCollectionSlug } from 'payload'

console.log(lockedDocumentsCollectionSlug) // 'payload-locked-documents'
```

### Functions

#### `getLockedDocumentsCollection(config: Config)`

Creates the internal collection configuration for tracking locked documents.

**Parameters:**
| Parameter | Type | Description |
|-----------|------|-------------|
| `config` | `Config` | The main PayloadCMS configuration object |

**Returns:** `CollectionConfig`

**Example:**
```typescript
import { getLockedDocumentsCollection } from 'payload'
import type { Config } from 'payload'

const config: Config = {
  collections: [/* your collections */],
  // ... other config
}

const lockedDocsCollection = getLockedDocumentsCollection(config)
// Returns internal collection configuration
```

#### `checkDocumentLockStatus(args: CheckDocumentLockStatusArgs)`

Utility function to check if a document is locked and throw an error if lock enforcement is requested.

**Parameters:**
| Parameter | Type | Description |
|-----------|------|-------------|
| `args.req` | `PayloadRequest` | The Payload request object |
| `args.collectionSlug?` | `string` | Collection slug (for collection documents) |
| `args.globalSlug?` | `string` | Global slug (for global documents) |
| `args.id?` | `string \| number` | Document ID (required for collections) |
| `args.overrideLock?` | `boolean` | Whether to override lock protection (default: true) |
| `args.lockDurationDefault?` | `number` | Default lock duration in seconds (default: 300) |
| `args.lockErrorMessage?` | `string` | Custom error message for locked documents |

**Returns:** `Promise<void>`

**Example:**
```typescript
import { checkDocumentLockStatus } from 'payload'

// Check collection document
await checkDocumentLockStatus({
  req,
  collectionSlug: 'posts',
  id: '12345',
  overrideLock: false, // Enforce lock protection
  lockErrorMessage: 'Post is being edited by another user'
})

// Check global document
await checkDocumentLockStatus({
  req,
  globalSlug: 'site-settings',
  overrideLock: false,
  lockDurationDefault: 600 // 10 minutes
})
```

### Error Classes

#### `Locked`

Error thrown when attempting to modify a locked document with `overrideLock: false`.

**Properties:**
- `name`: 'Locked'
- `status`: 423 (HTTP LOCKED status code)
- `message`: Custom error message

**Example:**
```typescript
import { Locked } from 'payload'

try {
  await payload.update({
    collection: 'posts',
    id: '123',
    data: { title: 'New Title' },
    overrideLock: false
  })
} catch (error) {
  if (error instanceof Locked) {
    console.log('Document is locked:', error.message)
    // Handle locked document scenario
  }
}
```

### TypeScript Types

```typescript
// Lock configuration type
type LockDocumentsConfig = {
  duration: number
} | false

// Check lock status arguments
interface CheckDocumentLockStatusArgs {
  req: PayloadRequest
  collectionSlug?: string
  globalSlug?: string  
  id?: string | number
  overrideLock?: boolean
  lockDurationDefault?: number
  lockErrorMessage?: string
}

// Internal locked document structure
interface LockedDocumentRecord {
  id: string
  document?: {
    relationTo: string
    value: string | number
  }
  globalSlug?: string
  user: {
    relationTo: string
    value: string | number
  }
  createdAt: Date
  updatedAt: Date
}
```

## Integrations

### PayloadCMS Collections

The locked documents system integrates with all PayloadCMS collections:

- **Document Operations**: Automatically checks locks during update and delete operations
- **Admin Interface**: Provides visual feedback and lock takeover options in the admin panel
- **Access Control**: Respects existing access control while adding lock-based protection

### Database Integration

The system creates and manages the `payload-locked-documents` collection:

- **Schema**: Automatically configured based on your collections and auth setup
- **Indexes**: Optimized queries with indexes on document relationships and global slugs  
- **Cleanup**: Automatic removal of expired locks during operations

### Authentication Integration

Document locking requires authentication and integrates with:

- **User Sessions**: Tracks which user holds each lock
- **Auth Collections**: Automatically detects and supports all authenticated collections
- **Permissions**: Respects existing user permissions while adding concurrency control

## Troubleshooting

### Common Issues

#### Document Always Shows as Locked

**Problem:** Users report that documents appear locked even when no one is editing them.

**Solution:**
1. Check if lock duration is too long for your use case
2. Clear orphaned locks from the database
3. Verify system clock synchronization

**Example:**
```typescript
// Clear all expired locks manually
await payload.delete({
  collection: 'payload-locked-documents',
  where: {
    updatedAt: {
      less_than: new Date(Date.now() - 300000) // 5 minutes ago
    }
  }
})
```

#### Lock Override Not Working

**Problem:** Setting `overrideLock: true` doesn't bypass locks as expected.

**Solution:**
Ensure you're setting the parameter correctly in the operation:

**Example:**
```typescript
// ❌ Wrong - this still enforces locks
await payload.update({
  collection: 'posts',
  id: '123', 
  data: { title: 'New Title' },
  overrideLock: false // This enforces locks!
})

// ✅ Correct - this bypasses locks
await payload.update({
  collection: 'posts',
  id: '123',
  data: { title: 'New Title' },
  overrideLock: true // This bypasses locks
})
```

#### Lock Errors in API Operations

**Problem:** Getting lock errors when using Local API or REST API operations.

**Solution:**
Handle lock errors gracefully and provide user feedback:

**Example:**
```typescript
import { Locked } from 'payload'

try {
  const result = await payload.update({
    collection: 'posts',
    id: docId,
    data: updateData,
    overrideLock: false
  })
  return { success: true, result }
} catch (error) {
  if (error instanceof Locked) {
    return {
      success: false,
      error: 'DOCUMENT_LOCKED',
      message: 'This document is being edited by another user',
      canOverride: userHasAdminRights
    }
  }
  throw error
}
```

### Debugging

Enable debug logging to troubleshoot locking issues:

```typescript
export default buildConfig({
  // ... other config
  collections: [
    {
      slug: 'posts',
      lockDocuments: {
        duration: 300
      },
      fields: [/* ... */]
    }
  ],
  onInit: async (payload) => {
    payload.logger.info('Document locking system initialized')
    
    // Log lock collection status
    const lockCollection = payload.collections['payload-locked-documents']
    if (lockCollection) {
      payload.logger.info('Lock tracking collection configured successfully')
    }
  }
})
```

Monitor locked documents in your database:

```typescript
// Query current locks
const currentLocks = await payload.find({
  collection: 'payload-locked-documents',
  depth: 2,
  sort: '-updatedAt'
})

console.log('Current document locks:', currentLocks.docs)
```

## Performance

### Performance Optimization

1. **Lock Duration Tuning**: Set appropriate lock durations based on typical editing sessions
2. **Database Indexes**: The system automatically creates indexes on relationship fields
3. **Cleanup Strategy**: Expired locks are cleaned up during normal operations
4. **Connection Pooling**: Use database connection pooling for high-concurrency scenarios

```typescript
// Optimize for high-frequency editing
export const FastEditCollection: CollectionConfig = {
  slug: 'quick-edits',
  lockDocuments: {
    duration: 60 // Short 1-minute locks for rapid editing
  },
  fields: [/* ... */]
}

// Optimize for long-form editing
export const LongFormCollection: CollectionConfig = {
  slug: 'articles',
  lockDocuments: {
    duration: 1800 // 30-minute locks for thorough editing
  },
  fields: [/* ... */]
}
```

## Security

### Security Considerations

1. **User Authentication**: Locking only works with authenticated users - ensure proper auth setup
2. **Access Control**: Document locks respect existing access control policies
3. **Lock Hijacking**: The "take over" functionality should be limited to appropriate user roles
4. **DoS Prevention**: Reasonable lock durations prevent indefinite resource locking

```typescript
// Secure lock configuration with role-based overrides
export const SecureCollection: CollectionConfig = {
  slug: 'sensitive-docs',
  access: {
    update: ({ req }) => {
      // Only editors and admins can edit
      return req.user?.role === 'editor' || req.user?.role === 'admin'
    }
  },
  lockDocuments: {
    duration: 300 // 5-minute locks
  },
  fields: [
    {
      name: 'content',
      type: 'richText',
      access: {
        update: ({ req }) => {
          // Additional field-level security
          return req.user?.role === 'admin'
        }
      }
    }
  ]
}
```

## Migration

### From Previous Versions

If upgrading from Payload 2.x:

1. **Automatic Migration**: Document locking is automatically configured in 3.x
2. **Configuration Changes**: Lock settings are now part of collection/global config
3. **Database Schema**: The lock tracking collection is created automatically

```typescript
// Payload 2.x style (deprecated)
// lockDocuments was a global setting

// Payload 3.x style (current)
export const Collection: CollectionConfig = {
  slug: 'posts',
  lockDocuments: {
    duration: 300
  },
  // ... other config
}
```

## Contributing

Found a bug or have a suggestion? [Open an issue](https://github.com/payloadcms/payload/issues) or submit a Pull Request.

## License

MIT License - see the [LICENSE](https://github.com/payloadcms/payload/blob/main/LICENSE) file for details.