---
title: User Preferences Core Module
label: Preferences Core
order: 60
desc: Internal PayloadCMS module providing user preferences infrastructure, collection configuration, and persistence for admin panel customizations.
keywords: [preferences, user, admin, persistence, collection, customization, ui, state, payload, database]
---

<Banner type="warning">
**Original Documentation**: The content below comes from [official PayloadCMS documentation](../../../docs/admin/preferences.mdx).
Further in the document, you'll find an extended, more detailed version of this documentation.
</Banner>

As your users interact with the [Admin Panel](./overview), you might want to store their preferences in a persistent manner, so that when they revisit the Admin Panel in a different session or from a different device, they can pick right back up where they left off.

Out of the box, Payload handles the persistence of your users' preferences in a handful of ways, including:

1. Columns in the Collection List View: their active state and order
1. The user's last active [Locale](../configuration/localization)
1. The "collapsed" state of `blocks`, `array`, and `collapsible` fields
1. The last-known state of the `Nav` component, etc.

<Banner type="warning">
  **Important:**

All preferences are stored on an individual user basis. Payload automatically recognizes the user
that is reading or setting a preference via all provided authentication methods.

</Banner>

## Use Cases

This API is used significantly for internal operations of the Admin Panel, as mentioned above. But, if you're building your own React components for use in the Admin Panel, you can allow users to set their own preferences in correspondence to their usage of your components. For example:

- If you have built a "color picker", you could "remember" the last used colors that the user has set for easy access next time
- If you've built a custom `Nav` component, and you've built in an "accordion-style" UI, you might want to store the `collapsed` state of each Nav collapsible item. This way, if an editor returns to the panel, their `Nav` state is persisted automatically
- You might want to store `recentlyAccessed` documents to give admin editors an easy shortcut back to their recently accessed documents on the `Dashboard` or similar
- Many other use cases exist. Invent your own! Give your editors an intelligent and persistent editing experience.

## Database

Payload automatically creates an internally used `payload-preferences` Collection that stores user preferences. Each document in the `payload-preferences` Collection contains the following shape:

| Key               | Value                                                             |
| ----------------- | ----------------------------------------------------------------- |
| `id`              | A unique ID for each preference stored.                           |
| `key`             | A unique `key` that corresponds to the preference.                |
| `user.value`      | The ID of the `user` that is storing its preference.              |
| `user.relationTo` | The `slug` of the Collection that the `user` is logged in as.     |
| `value`           | The value of the preference. Can be any data shape that you need. |
| `createdAt`       | A timestamp of when the preference was created.                   |
| `updatedAt`       | A timestamp set to the last time the preference was updated.      |

## APIs

Preferences are available to both [GraphQL](/docs/graphql/overview#preferences) and [REST](/docs/rest-api/overview#preferences) APIs.

## Adding or reading Preferences in your own components

The Payload Admin Panel offers a `usePreferences` hook. The hook is only meant for use within the Admin Panel itself. It provides you with two methods:

#### `getPreference`

This async method provides an easy way to retrieve a user's preferences by `key`. It will return a promise containing the resulting preference value.

**Arguments**

- `key`: the `key` of your preference to retrieve.

#### `setPreference`

Also async, this method provides you with an easy way to set a user preference. It returns `void`.

**Arguments:**

- `key`: the `key` of your preference to set.
- `value`: the `value` of your preference that you're looking to set.

## Example

Here is an example for how you can utilize `usePreferences` within your custom Admin Panel components. Note - this example is not fully useful and is more just a reference for how to utilize the Preferences API. In this case, we are demonstrating how to set and retrieve a user's last used colors history within a `ColorPicker` or similar type component.

```tsx
'use client'
import React, { Fragment, useState, useEffect, useCallback } from 'react'
import { usePreferences } from '@payloadcms/ui'

const lastUsedColorsPreferenceKey = 'last-used-colors'

export function CustomComponent() {
  const { getPreference, setPreference } = usePreferences()

  // Store the last used colors in local state
  const [lastUsedColors, setLastUsedColors] = useState([])

  // Callback to add a color to the last used colors
  const updateLastUsedColors = useCallback(
    (color) => {
      // First, check if color already exists in last used colors.
      // If it already exists, there is no need to update preferences
      const colorAlreadyExists = lastUsedColors.indexOf(color) > -1

      if (!colorAlreadyExists) {
        const newLastUsedColors = [...lastUsedColors, color]

        setLastUsedColors(newLastUsedColors)
        setPreference(lastUsedColorsPreferenceKey, newLastUsedColors)
      }
    },
    [lastUsedColors, setPreference],
  )

  // Retrieve preferences on component mount
  // This will only be run one time, because the `getPreference` method never changes
  useEffect(() => {
    const asyncGetPreference = async () => {
      const lastUsedColorsFromPreferences = await getPreference(
        lastUsedColorsPreferenceKey,
      )
      setLastUsedColors(lastUsedColorsFromPreferences)
    }

    asyncGetPreference()
  }, [getPreference])

  return (
    <div>
      <button type="button" onClick={() => updateLastUsedColors('red')}>
        Use red
      </button>
      <button type="button" onClick={() => updateLastUsedColors('blue')}>
        Use blue
      </button>
      <button type="button" onClick={() => updateLastUsedColors('purple')}>
        Use purple
      </button>
      <button type="button" onClick={() => updateLastUsedColors('yellow')}>
        Use yellow
      </button>
      {lastUsedColors && (
        <Fragment>
          <h5>Last used colors:</h5>
          <ul>
            {lastUsedColors?.map((color) => <li key={color}>{color}</li>)}
          </ul>
        </Fragment>
      )}
    </div>
  )
}
```

---

## 📚 Extended Documentation

<Banner type="success">
**Note**: The documentation below has been automatically generated based on source code analysis and contains more detailed information than the original documentation above.
</Banner>

## Detailed Overview

The PayloadCMS User Preferences Core Module provides the foundational infrastructure for storing and managing user-specific settings and UI state within the PayloadCMS admin interface. This internal system creates and manages a specialized collection that persists user preferences across sessions, enabling a personalized and consistent editing experience.

The module automatically creates the `payload-preferences` collection that stores key-value pairs associated with specific users. This system supports complex data structures, automatic cleanup when users are deleted, and provides both REST and GraphQL endpoints for preference management. The preferences system is deeply integrated with the admin interface to remember field collapse states, column configurations, navigation preferences, and custom component states.

Key benefits include persistent user experience across sessions, automatic user-scoped data isolation, support for complex nested preference structures, seamless integration with admin UI components, and comprehensive API access for both built-in and custom functionality.

<Banner type="info">
The package is open-source. [View source code](https://github.com/payloadcms/payload/tree/main/packages/payload/src/preferences). Need help? [Community Help](https://payloadcms.com/community-help).
</Banner>

## System Requirements

- **PayloadCMS**: ^3.0.0
- **Node.js**: >=18.0.0
- **Database**: MongoDB, PostgreSQL, or SQLite
- **Authentication**: Requires at least one authenticated collection

## Installation

The preferences module is included automatically with PayloadCMS core and doesn't require separate installation:

```bash
# npm
npm install payload

# yarn  
yarn add payload

# pnpm
pnpm add payload
```

## Quick Start

The preferences system works automatically once you have authentication configured. Access preferences through the admin hooks or REST/GraphQL APIs:

```typescript
// In React components within the admin panel
import { usePreferences } from '@payloadcms/ui'

export function MyCustomComponent() {
  const { getPreference, setPreference } = usePreferences()
  
  // Get a preference
  const handleLoad = async () => {
    const value = await getPreference('my-custom-key')
    console.log('Current preference:', value)
  }
  
  // Set a preference
  const handleSave = async () => {
    await setPreference('my-custom-key', { 
      theme: 'dark', 
      layout: 'grid' 
    })
  }
  
  return (
    <div>
      <button onClick={handleLoad}>Load Preference</button>
      <button onClick={handleSave}>Save Preference</button>
    </div>
  )
}
```

### REST API Usage

```typescript
// GET a preference
const response = await fetch('/api/preferences/my-preference-key', {
  headers: { 
    'Authorization': `Bearer ${token}`,
    'Content-Type': 'application/json'
  }
})
const preference = await response.json()

// POST (create/update) a preference
await fetch('/api/preferences/my-preference-key', {
  method: 'POST',
  headers: { 
    'Authorization': `Bearer ${token}`,
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({
    value: { setting1: 'value1', setting2: 42 }
  })
})

// DELETE a preference
await fetch('/api/preferences/my-preference-key', {
  method: 'DELETE',
  headers: { 
    'Authorization': `Bearer ${token}`
  }
})
```

## Detailed Configuration

### Internal Collection Structure

The preferences system automatically creates the `payload-preferences` collection with the following schema:

```typescript
{
  slug: 'payload-preferences',
  access: {
    delete: ({ req }) => req.user && { 'user.value': { equals: req.user.id } },
    read: ({ req }) => req.user && { 'user.value': { equals: req.user.id } }
  },
  admin: { hidden: true },
  fields: [
    {
      name: 'user',
      type: 'relationship',
      relationTo: [/* all auth-enabled collections */],
      required: true,
      index: true
    },
    {
      name: 'key',
      type: 'text',
      index: true
    },
    {
      name: 'value',
      type: 'json'
    }
  ],
  lockDocuments: false
}
```

### Configuration Schema

```typescript
// Core preference structure
interface PreferenceDocument {
  id: string
  key: string
  user: {
    relationTo: string
    value: string | number
  }
  value: any
  createdAt: string
  updatedAt: string
}

// Request types
interface PreferenceRequest {
  key: string
  req: PayloadRequest
  user: PayloadRequest['user']
  overrideAccess?: boolean
}

interface PreferenceUpdateRequest extends PreferenceRequest {
  value: unknown
}

// Built-in preference types
interface CollectionPreferences {
  columns?: Array<{
    accessor: string
    active: boolean
  }>
  editViewType?: 'default' | 'live-preview'
  groupBy?: string
  limit?: number
  preset?: string | number
  sort?: string
}

interface DocumentPreferences {
  fields: {
    [key: string]: {
      collapsed: string[]
      tabIndex: number
    }
  }
}
```

## Usage Guides

### Managing Collection View Preferences

Store and retrieve user preferences for collection list views:

```typescript
import { usePreferences } from '@payloadcms/ui'

export function CollectionViewCustomizer() {
  const { getPreference, setPreference } = usePreferences()
  
  const handleSaveViewPreferences = async (collectionSlug: string) => {
    const preferences = {
      columns: [
        { accessor: 'title', active: true },
        { accessor: 'status', active: true },
        { accessor: 'createdAt', active: false }
      ],
      limit: 25,
      sort: '-createdAt',
      groupBy: 'status'
    }
    
    await setPreference(`collection-${collectionSlug}`, preferences)
  }
  
  const handleLoadViewPreferences = async (collectionSlug: string) => {
    const preferences = await getPreference(`collection-${collectionSlug}`)
    return preferences || {
      columns: [],
      limit: 10,
      sort: 'id'
    }
  }
  
  return (
    <div>
      <button onClick={() => handleSaveViewPreferences('posts')}>
        Save Posts View
      </button>
      <button onClick={() => handleLoadViewPreferences('posts')}>
        Load Posts View
      </button>
    </div>
  )
}
```

### Custom Field State Persistence

Manage complex field state preferences for custom components:

```typescript
import { usePreferences } from '@payloadcms/ui'
import { useState, useEffect } from 'react'

interface CustomFieldPreferences {
  layout: 'grid' | 'list'
  itemsPerPage: number
  filters: {
    category: string[]
    status: string[]
  }
  sortBy: string
  sortOrder: 'asc' | 'desc'
}

export function CustomFieldComponent() {
  const { getPreference, setPreference } = usePreferences()
  const [fieldState, setFieldState] = useState<CustomFieldPreferences>({
    layout: 'grid',
    itemsPerPage: 12,
    filters: { category: [], status: [] },
    sortBy: 'name',
    sortOrder: 'asc'
  })
  
  const preferenceKey = 'custom-field-gallery'
  
  // Load preferences on mount
  useEffect(() => {
    const loadPreferences = async () => {
      const saved = await getPreference(preferenceKey)
      if (saved) {
        setFieldState(prev => ({ ...prev, ...saved }))
      }
    }
    loadPreferences()
  }, [getPreference])
  
  // Save preferences when state changes
  const savePreferences = async (newState: Partial<CustomFieldPreferences>) => {
    const updated = { ...fieldState, ...newState }
    setFieldState(updated)
    await setPreference(preferenceKey, updated)
  }
  
  return (
    <div>
      <div>
        Layout:
        <button 
          onClick={() => savePreferences({ layout: 'grid' })}
          disabled={fieldState.layout === 'grid'}
        >
          Grid
        </button>
        <button 
          onClick={() => savePreferences({ layout: 'list' })}
          disabled={fieldState.layout === 'list'}
        >
          List
        </button>
      </div>
      
      <div>
        Items per page:
        <select 
          value={fieldState.itemsPerPage}
          onChange={(e) => savePreferences({ itemsPerPage: Number(e.target.value) })}
        >
          <option value={6}>6</option>
          <option value={12}>12</option>
          <option value={24}>24</option>
          <option value={48}>48</option>
        </select>
      </div>
      
      <div>Current layout: {fieldState.layout}</div>
      <div>Items per page: {fieldState.itemsPerPage}</div>
    </div>
  )
}
```

### Advanced Patterns

#### Scoped Preferences with Context

Create preferences that are scoped to specific contexts or documents:

```typescript
import { usePreferences } from '@payloadcms/ui'

export function DocumentScopedPreferences({ documentId, collectionSlug }: {
  documentId: string
  collectionSlug: string
}) {
  const { getPreference, setPreference } = usePreferences()
  
  const getScopedKey = (key: string) => `${collectionSlug}-${documentId}-${key}`
  
  const saveFieldCollapsedState = async (fieldPath: string, collapsed: boolean) => {
    const key = getScopedKey('field-states')
    const existing = await getPreference(key) || {}
    
    await setPreference(key, {
      ...existing,
      [fieldPath]: { collapsed, updatedAt: new Date().toISOString() }
    })
  }
  
  const getFieldCollapsedState = async (fieldPath: string): Promise<boolean> => {
    const key = getScopedKey('field-states')
    const fieldStates = await getPreference(key)
    return fieldStates?.[fieldPath]?.collapsed || false
  }
  
  return {
    saveFieldCollapsedState,
    getFieldCollapsedState
  }
}
```

#### Preferences Migration and Cleanup

Handle preferences migration and cleanup:

```typescript
import { usePreferences } from '@payloadcms/ui'

export function PreferencesMigration() {
  const { getPreference, setPreference } = usePreferences()
  
  // Migrate old preference format to new format
  const migratePreferences = async () => {
    const oldKey = 'legacy-settings'
    const newKey = 'modern-settings-v2'
    
    const oldPrefs = await getPreference(oldKey)
    if (oldPrefs && !await getPreference(newKey)) {
      // Transform old format to new format
      const migratedPrefs = {
        version: 2,
        settings: {
          theme: oldPrefs.darkMode ? 'dark' : 'light',
          layout: oldPrefs.compactView ? 'compact' : 'comfortable',
          // ... other transformations
        },
        migratedAt: new Date().toISOString(),
        migratedFrom: oldKey
      }
      
      await setPreference(newKey, migratedPrefs)
      console.log('Preferences migrated successfully')
    }
  }
  
  // Cleanup old or invalid preferences
  const cleanupPreferences = async () => {
    const keysToCheck = [
      'temp-settings',
      'draft-preferences',
      'expired-cache'
    ]
    
    for (const key of keysToCheck) {
      const pref = await getPreference(key)
      if (pref && pref.expiresAt && new Date(pref.expiresAt) < new Date()) {
        // Delete expired preferences
        await fetch(`/api/preferences/${key}`, { method: 'DELETE' })
      }
    }
  }
  
  return { migratePreferences, cleanupPreferences }
}
```

## API Reference

### Constants

#### `preferencesCollectionSlug`

- **Value**: `'payload-preferences'`
- **Description**: The slug of the internal collection used to store user preferences

```typescript
import { preferencesCollectionSlug } from 'payload'

console.log(preferencesCollectionSlug) // 'payload-preferences'
```

### Functions

#### `getPreferencesCollection(config: Config)`

Creates the internal collection configuration for storing user preferences.

**Parameters:**
| Parameter | Type | Description |
|-----------|------|-------------|
| `config` | `Config` | The main PayloadCMS configuration object |

**Returns:** `CollectionConfig`

**Example:**
```typescript
import { getPreferencesCollection } from 'payload'
import type { Config } from 'payload'

const config: Config = {
  collections: [/* your collections */],
  // ... other config
}

const preferencesCollection = getPreferencesCollection(config)
// Returns internal collection configuration with user-scoped access
```

#### `deleteUserPreferences(args: DeleteUserPreferencesArgs)`

Utility function to clean up preferences when users are deleted.

**Parameters:**
| Parameter | Type | Description |
|-----------|------|-------------|
| `args.collectionConfig` | `SanitizedCollectionConfig` | The collection configuration |
| `args.ids` | `(string \| number)[]` | Array of user IDs to delete preferences for |
| `args.payload` | `Payload` | The Payload instance |
| `args.req` | `PayloadRequest` | The request object |

**Returns:** `Promise<void>`

**Example:**
```typescript
import { deleteUserPreferences } from 'payload'

// Called automatically when users are deleted
await deleteUserPreferences({
  collectionConfig: usersCollection,
  ids: ['user1', 'user2'],
  payload,
  req
})
```

### Operations

#### `findOne(args: PreferenceRequest)`

Find a specific user preference by key.

**Parameters:**
| Parameter | Type | Description |
|-----------|------|-------------|
| `args.key` | `string` | The preference key to find |
| `args.req` | `PayloadRequest` | The request object |
| `args.user` | `PayloadRequest['user']` | The authenticated user |

**Returns:** `Promise<PreferenceDocument | null>`

#### `update(args: PreferenceUpdateRequest)`

Create or update a user preference.

**Parameters:**
| Parameter | Type | Description |
|-----------|------|-------------|
| `args.key` | `string` | The preference key |
| `args.value` | `unknown` | The preference value |
| `args.req` | `PayloadRequest` | The request object |
| `args.user` | `PayloadRequest['user']` | The authenticated user |

**Returns:** `Promise<PreferenceDocument>`

#### `deleteOperation(args: PreferenceRequest)`

Delete a user preference.

**Parameters:**
| Parameter | Type | Description |
|-----------|------|-------------|
| `args.key` | `string` | The preference key to delete |
| `args.req` | `PayloadRequest` | The request object |
| `args.user` | `PayloadRequest['user']` | The authenticated user |

**Returns:** `Promise<PreferenceDocument>`

### TypeScript Types

```typescript
// Core request types
interface PreferenceRequest {
  key: string
  req: PayloadRequest
  user: PayloadRequest['user']
  overrideAccess?: boolean
}

interface PreferenceUpdateRequest extends PreferenceRequest {
  value: unknown
}

// Built-in preference types
type CollapsedPreferences = string[]

type TabsPreferences = Array<{
  [path: string]: number
}>

interface InsideFieldsPreferences {
  collapsed: CollapsedPreferences
  tabIndex: number
}

interface FieldsPreferences {
  [key: string]: InsideFieldsPreferences
}

interface DocumentPreferences {
  fields: FieldsPreferences
}

interface ColumnPreference {
  accessor: string
  active: boolean
}

interface CollectionPreferences {
  columns?: ColumnPreference[]
  editViewType?: 'default' | 'live-preview'
  groupBy?: string
  limit?: number
  preset?: DefaultDocumentIDType
  sort?: string
}
```

## Integrations

### Admin Interface Integration

The preferences system is deeply integrated with PayloadCMS admin components:

- **Field Components**: Automatically saves collapse states for array, block, and collapsible fields
- **Collection Lists**: Persists column visibility, sorting, and pagination preferences
- **Navigation**: Remembers expanded/collapsed state of navigation groups
- **Locale Selection**: Stores the user's last selected locale
- **Custom Components**: Provides hooks for custom component preferences

### Database Integration

The system creates and manages the `payload-preferences` collection:

- **Schema**: Automatically configured with proper relationships to auth collections
- **Access Control**: User-scoped access ensuring privacy and data isolation
- **Indexes**: Optimized queries with indexes on user relationships and preference keys
- **Cleanup**: Automatic removal of preferences when users are deleted

### Authentication Integration

Preferences require authentication and integrate with:

- **User Sessions**: Automatically associates preferences with the authenticated user
- **Multi-Collection Auth**: Supports preferences across different authenticated collections
- **Access Control**: Respects user permissions while providing preference access
- **Session Management**: Preferences persist across different authentication sessions

## Troubleshooting

### Common Issues

#### Preferences Not Persisting

**Problem:** User preferences are not being saved or are lost between sessions.

**Solution:**
1. Verify the user is properly authenticated
2. Check database connectivity and permissions
3. Ensure the preference key is valid and consistent

**Example:**
```typescript
// ❌ Wrong - inconsistent keys
await setPreference('user-theme', 'dark')
const theme = await getPreference('userTheme') // Won't find it!

// ✅ Correct - consistent keys
await setPreference('user-theme', 'dark')
const theme = await getPreference('user-theme') // Will work
```

#### JSON Validation Errors

**Problem:** Getting "Invalid JSON" errors when saving preferences.

**Solution:**
Ensure your preference values are JSON serializable:

**Example:**
```typescript
// ❌ Wrong - functions and undefined values aren't serializable
await setPreference('settings', {
  callback: () => console.log('test'),
  value: undefined,
  date: new Date() // This will be stringified
})

// ✅ Correct - JSON serializable values
await setPreference('settings', {
  theme: 'dark',
  count: 42,
  enabled: true,
  date: new Date().toISOString(),
  options: ['option1', 'option2']
})
```

#### Access Control Issues

**Problem:** Users can see or modify other users' preferences.

**Solution:**
The system automatically enforces user-scoped access, but verify your authentication:

**Example:**
```typescript
// Check user authentication before accessing preferences
export function MyComponent() {
  const { user } = useAuth()
  const { getPreference, setPreference } = usePreferences()
  
  if (!user) {
    return <div>Please log in to access preferences</div>
  }
  
  // Preferences are automatically scoped to the authenticated user
  const handleGetPreference = async () => {
    const pref = await getPreference('my-key')
    // Will only return preferences for the current user
  }
  
  return <button onClick={handleGetPreference}>Get Preference</button>
}
```

### Debugging

Enable debug logging to troubleshoot preferences issues:

```typescript
// Check current user context
export function PreferencesDebugger() {
  const { getPreference } = usePreferences()
  const { user } = useAuth()
  
  const debugPreferences = async () => {
    console.log('Current user:', user)
    
    // Try to get a test preference
    try {
      const testPref = await getPreference('debug-test')
      console.log('Test preference:', testPref)
    } catch (error) {
      console.error('Error accessing preferences:', error)
    }
  }
  
  return <button onClick={debugPreferences}>Debug Preferences</button>
}
```

Monitor preferences in your database:

```typescript
// Query current preferences for debugging
const debugUserPreferences = async (payload: Payload, userId: string) => {
  const preferences = await payload.find({
    collection: 'payload-preferences',
    where: {
      'user.value': { equals: userId }
    },
    depth: 0
  })
  
  console.log(`User ${userId} has ${preferences.totalDocs} preferences:`)
  preferences.docs.forEach(pref => {
    console.log(`- ${pref.key}: ${JSON.stringify(pref.value)}`)
  })
  
  return preferences
}
```

## Performance

### Performance Optimization

1. **Batch Preference Updates**: Minimize individual API calls by batching related preferences
2. **Caching Strategy**: Consider client-side caching for frequently accessed preferences  
3. **Database Indexing**: The system automatically creates indexes on user and key fields
4. **Cleanup Strategy**: Regularly clean up obsolete or unused preferences

```typescript
// Batch multiple preference updates
export function BatchPreferenceUpdate() {
  const { setPreference } = usePreferences()
  
  const saveMultiplePreferences = async (preferences: Record<string, any>) => {
    // Instead of multiple individual calls, consider batching
    const updates = Object.entries(preferences).map(([key, value]) =>
      setPreference(key, value)
    )
    
    await Promise.all(updates)
  }
  
  const handleSaveDashboardLayout = async () => {
    await saveMultiplePreferences({
      'dashboard-layout': 'grid',
      'dashboard-columns': 3,
      'dashboard-sort': 'name',
      'dashboard-filters': ['active', 'recent']
    })
  }
  
  return <button onClick={handleSaveDashboardLayout}>Save Layout</button>
}
```

## Security

### Security Considerations

1. **User Isolation**: Preferences are automatically scoped to individual users
2. **Input Validation**: JSON validation prevents malformed data storage
3. **Access Control**: Built-in access control prevents cross-user preference access
4. **Data Sanitization**: Ensure preference values don't contain sensitive information

```typescript
// Secure preference handling
export function SecurePreferencesComponent() {
  const { setPreference, getPreference } = usePreferences()
  
  const saveSecurePreference = async (key: string, value: any) => {
    // Sanitize value before saving
    const sanitizedValue = {
      ...value,
      // Remove any potentially sensitive data
      password: undefined,
      token: undefined,
      secret: undefined,
      // Limit size to prevent abuse
      data: JSON.stringify(value.data || {}).substring(0, 10000)
    }
    
    await setPreference(key, sanitizedValue)
  }
  
  const getSecurePreference = async (key: string) => {
    const value = await getPreference(key)
    
    // Always validate returned data
    if (value && typeof value === 'object') {
      return value
    }
    
    return null
  }
  
  return (
    <div>
      <button onClick={() => saveSecurePreference('settings', { theme: 'dark' })}>
        Save Secure Preference
      </button>
    </div>
  )
}
```

## Migration

### Migrating Existing Preferences

When updating preference structures, handle migration gracefully:

```typescript
// Preference migration utility
export function PreferencesMigrationHandler() {
  const { getPreference, setPreference } = usePreferences()
  
  const migrateV1ToV2 = async () => {
    const v1Key = 'user-settings'
    const v2Key = 'user-settings-v2'
    
    const v1Settings = await getPreference(v1Key)
    if (v1Settings && !await getPreference(v2Key)) {
      const v2Settings = {
        version: 2,
        // Migrate structure
        ui: {
          theme: v1Settings.darkMode ? 'dark' : 'light',
          density: v1Settings.compact ? 'compact' : 'comfortable'
        },
        collections: v1Settings.collections || {},
        migratedAt: new Date().toISOString()
      }
      
      await setPreference(v2Key, v2Settings)
      
      // Optionally remove old preference
      // await deletePreference(v1Key)
    }
  }
  
  return { migrateV1ToV2 }
}
```

## Contributing

Found a bug or have a suggestion? [Open an issue](https://github.com/payloadcms/payload/issues) or submit a Pull Request.

## License

MIT License - see the [LICENSE](https://github.com/payloadcms/payload/blob/main/LICENSE) file for details.