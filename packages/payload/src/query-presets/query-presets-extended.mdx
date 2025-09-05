---
title: Query Presets Core Module
label: Query Presets Core
order: 10
desc: Internal PayloadCMS module providing query preset infrastructure, collection configuration, and advanced access control for saved filters and views.
keywords: [query, presets, filters, collections, access, constraints, sharing, admin, views, database]
---

<Banner type="warning">
**Original Documentation**: The content below comes from [official PayloadCMS documentation](../../../docs/query-presets/overview.mdx).
Further in the document, you'll find an extended, more detailed version of this documentation.
</Banner>

Query Presets allow you to save and share filters, columns, and sort orders for your [Collections](../configuration/collections). This is useful for reusing common or complex filtering patterns and/or sharing them across your team.

Each Query Preset is saved as a new record in the database under the `payload-query-presets` collection. This allows for an endless number of preset configurations, where the users of your app define the presets that are most useful to them, rather than being hard coded into the Payload Config.

Within the [Admin Panel](../admin/overview), Query Presets are applied to the List View. When enabled, new controls are displayed for users to manage presets. Once saved, these presets can be loaded up at any time and optionally shared with others.

To enable Query Presets on a Collection, use the `enableQueryPresets` property in your [Collection Config](../configuration/collections):

```ts
import type { CollectionConfig } from 'payload'

export const MyCollection: CollectionConfig = {
  // ...
  // highlight-start
  enableQueryPresets: true,
  // highlight-end
}
```

## Config Options

While not required, you may want to customize the behavior of Query Presets to suit your needs, such as add custom labels or access control rules.

Settings for Query Presets are managed on the `queryPresets` property at the root of your [Payload Config](../configuration/overview):

```ts
import { buildConfig } from 'payload'

const config = buildConfig({
  // ...
  // highlight-start
  queryPresets: {
    // ...
  },
  // highlight-end
})
```

The following options are available for Query Presets:

| Option              | Description                                                                                                                     |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------------- |
| `access`            | Used to define custom collection-level access control that applies to all presets. [More details](#access-control).             |
| `filterConstraints` | Used to define which constraints are available to users when managing presets. [More details](#constraint-access-control).      |
| `constraints`       | Used to define custom document-level access control that apply to individual presets. [More details](#document-access-control). |
| `labels`            | Custom labels to use for the Query Presets collection.                                                                          |

## Access Control

Query Presets are subject to the same [Access Control](../access-control/overview) as the rest of Payload. This means you can use the same patterns you are already familiar with to control who can read, update, and delete presets.

Access Control for Query Presets can be customized in two ways:

1. [Collection Access Control](#collection-access-control): Applies to all presets. These rules are not controllable by the user and are statically defined in the config.
2. [Document Access Control](#document-access-control): Applies to each individual preset. These rules are controllable by the user and are dynamically defined on each record in the database.

### Collection Access Control

Collection-level access control applies to _all_ presets within the Query Presets collection. Users cannot control these rules, they are written statically in your config.

To add Collection Access Control, use the `queryPresets.access` property in your [Payload Config](../configuration/overview):

```ts
import { buildConfig } from 'payload'

const config = buildConfig({
  // ...
  queryPresets: {
    // ...
    // highlight-start
    access: {
      read: ({ req: { user } }) =>
        user ? user?.roles?.some((role) => role === 'admin') : false,
      update: ({ req: { user } }) =>
        user ? user?.roles?.some((role) => role === 'admin') : false,
    },
    // highlight-end
  },
})
```

This example restricts all Query Presets to users with the role of `admin`.

<Banner type="warning">
  **Note:** Custom access control will override the defaults on this collection,
  including the requirement for a user to be authenticated. Be sure to include
  any necessary checks in your custom rules unless you intend on making these
  publicly accessible.
</Banner>

### Document Access Control

You can also define access control rules that apply to each specific preset. Users have the ability to define and modify these rules on the fly as they manage presets. These are saved dynamically in the database on each record.

When a user manages a preset, document-level access control options will be available to them in the Admin Panel for each operation.

By default, Payload provides a set of sensible defaults for all Query Presets, but you can customize these rules to suit your needs:

- **Only Me**: Only the user who created the preset can read, update, and delete it.
- **Everyone**: All users can read, update, and delete the preset.
- **Specific Users**: Only select users can read, update, and delete the preset.

#### Custom Access Control

You can augment the default access control rules with your own custom rules. This can be useful for creating more complex access control patterns that the defaults don't provide, such as for RBAC.

Adding custom access control rules requires:

1. A label to display in the dropdown
2. A set of fields to conditionally render when that option is selected
3. A function that returns the access control rules for that option

To do this, use the `queryPresets.constraints` property in your [Payload Config](../configuration/overview).

```ts
import { buildConfig } from 'payload'

const config = buildConfig({
  // ...
  queryPresets: {
    // ...
    // highlight-start
    constraints: {
      read: [
        {
          label: 'Specific Roles',
          value: 'specificRoles',
          fields: [
            {
              name: 'roles',
              type: 'select',
              hasMany: true,
              options: [
                { label: 'Admin', value: 'admin' },
                { label: 'User', value: 'user' },
              ],
            },
          ],
          access: ({ req: { user } }) => ({
            'access.read.roles': {
              in: [user?.roles],
            },
          }),
        },
      ],
    },
    // highlight-end
  },
})
```

In this example, we've added a new option called `Specific Roles` that allows users to select from a list of roles. When this option is selected, the user will be prompted to select one or more roles from a list of options. The access control rule for this option is that the user operating on the preset must have one of the selected roles.

<Banner type="warning">
  **Note:** Payload places your custom fields into the `access[operation]` field
  group, so your rules will need to reflect this.
</Banner>

The following options are available for each constraint:

| Option   | Description                                                              |
| -------- | ------------------------------------------------------------------------ |
| `label`  | The label to display in the dropdown for this constraint.                |
| `value`  | The value to store in the database when this constraint is selected.     |
| `fields` | An array of fields to render when this constraint is selected.           |
| `access` | A function that determines the access control rules for this constraint. |

### Constraint Access Control

Used to dynamically filter which constraints are available based on the current user, document data, or other criteria.

Some examples of this might include:

- Ensuring that only "admins" are allowed to make a preset available to "everyone"
- Preventing the "onlyMe" option from being selected based on a hypothetical "disablePrivatePresets" checkbox

When a user lacks the permission to set a constraint, the option will either be hidden from them, or disabled if it is already saved to that preset.

To do this, you can use the `filterConstraints` property in your [Payload Config](../configuration/overview):

```ts
import { buildConfig } from 'payload'

const config = buildConfig({
  // ...
  queryPresets: {
    // ...
    // highlight-start
    filterConstraints: ({ req, options }) =>
      !req.user?.roles?.includes('admin')
        ? options.filter(
            (option) =>
              (typeof option === 'string' ? option : option.value) !==
              'everyone',
          )
        : options,
    // highlight-end
  },
})
```

The `filterConstraints` function receives the same arguments as [`filterOptions`](../fields/select#filteroptions) in the [Select field](../fields/select).

---

## 📚 Extended Documentation

<Banner type="success">
**Note**: The documentation below has been automatically generated based on source code analysis and contains more detailed information than the original documentation above.
</Banner>

## Detailed Overview

The PayloadCMS Query Presets Core Module provides a comprehensive system for creating, managing, and sharing saved queries, filters, and view configurations within the PayloadCMS admin interface. This internal system creates and manages the `payload-query-presets` collection, enabling users to save complex filtering criteria, column configurations, and sorting preferences that can be reused and shared across team members.

The module implements sophisticated access control mechanisms with both collection-level and document-level permissions, automatic lockout prevention to ensure users don't accidentally remove their own access, and flexible constraint systems that can be customized for different organizational needs. It integrates deeply with the admin interface to provide seamless preset management directly within collection list views.

Key benefits include persistent complex query configurations, team collaboration through shared presets, flexible multi-level access control system, prevention of accidental access lockouts, seamless integration with existing collection views, and support for custom constraint types and business rules.

<Banner type="info">
The package is open-source. [View source code](https://github.com/payloadcms/payload/tree/main/packages/payload/src/query-presets). Need help? [Community Help](https://payloadcms.com/community-help).
</Banner>

## System Requirements

- **PayloadCMS**: ^3.0.0
- **Node.js**: >=18.0.0
- **Database**: MongoDB, PostgreSQL, or SQLite
- **Authentication**: Requires at least one authenticated collection

## Installation

The query presets module is included automatically with PayloadCMS core and doesn't require separate installation:

```bash
# npm
npm install payload

# yarn  
yarn add payload

# pnpm
pnpm add payload
```

## Quick Start

Enable query presets on your collections and configure basic access control:

```typescript
import type { CollectionConfig, Config } from 'payload'

// Enable query presets on a collection
export const Posts: CollectionConfig = {
  slug: 'posts',
  enableQueryPresets: true, // Enable preset functionality
  fields: [
    { name: 'title', type: 'text' },
    { name: 'status', type: 'select', options: ['draft', 'published'] },
    { name: 'category', type: 'relationship', relationTo: 'categories' },
  ]
}

// Configure global query preset settings
export const config: Config = {
  collections: [Posts],
  queryPresets: {
    // Optional: Custom labels
    labels: {
      singular: 'Saved Filter',
      plural: 'Saved Filters'
    },
    // Optional: Collection-level access control
    access: {
      read: ({ req }) => Boolean(req.user), // Require authentication
      update: ({ req }) => req.user?.role === 'admin' // Admin-only updates
    }
  }
}
```

### Basic Usage in Admin Interface

Once enabled, users can:

1. **Create Presets**: Apply filters and column configurations in the list view, then save as a preset
2. **Load Presets**: Select from saved presets to quickly apply complex query configurations
3. **Share Presets**: Configure access control to share presets with other users or teams
4. **Manage Presets**: Edit, delete, and modify access permissions for existing presets

## Detailed Configuration

### Main Options

#### `enableQueryPresets`

- **Type**: `boolean`
- **Default**: `false`
- **Required**: No
- **Applied to**: Collection configuration

Enables query preset functionality for a specific collection.

```typescript
export const MyCollection: CollectionConfig = {
  slug: 'my-collection',
  enableQueryPresets: true, // Enable presets for this collection
  fields: [/* ... */]
}
```

#### `queryPresets.access`

- **Type**: `Record<Operation, Access>`
- **Default**: `defaultAccess` (requires authentication)
- **Required**: No

Defines collection-level access control that applies to all query presets.

```typescript
queryPresets: {
  access: {
    create: ({ req }) => req.user?.role === 'admin',
    read: ({ req }) => Boolean(req.user),
    update: ({ req }) => req.user?.role === 'admin',
    delete: ({ req }) => req.user?.role === 'admin'
  }
}
```

#### `queryPresets.constraints`

- **Type**: `Record<ConstraintOperation, QueryPresetConstraint[]>`
- **Default**: Built-in constraints (everyone, onlyMe, specificUsers)
- **Required**: No

Defines custom document-level access control constraints that users can select.

```typescript
queryPresets: {
  constraints: {
    read: [
      {
        label: 'Department Members',
        value: 'departmentMembers',
        fields: [
          {
            name: 'department',
            type: 'select',
            options: [
              { label: 'Engineering', value: 'engineering' },
              { label: 'Marketing', value: 'marketing' },
              { label: 'Sales', value: 'sales' }
            ]
          }
        ],
        access: ({ req }) => {
          const user = req.user
          return {
            'access.read.department': {
              equals: user?.department
            }
          }
        }
      }
    ]
  }
}
```

#### `queryPresets.filterConstraints`

- **Type**: `(args: FilterOptionsArgs) => Option[]`
- **Default**: All available constraints
- **Required**: No

Dynamically filters which constraints are available to users based on context.

```typescript
queryPresets: {
  filterConstraints: ({ req, options }) => {
    const user = req.user
    
    // Only admins can create "everyone" presets
    if (user?.role !== 'admin') {
      return options.filter(option => 
        (typeof option === 'string' ? option : option.value) !== 'everyone'
      )
    }
    
    return options
  }
}
```

### Configuration Schema

```typescript
// Global query presets configuration
interface QueryPresetsConfig {
  access?: Record<Operation, Access>
  constraints?: Record<ConstraintOperation, QueryPresetConstraint[]>
  filterConstraints?: (args: FilterOptionsArgs) => Option[]
  labels?: {
    singular?: string
    plural?: string
  }
}

// Individual query preset structure
interface QueryPreset {
  id: string | number
  title: string
  isShared: boolean
  relatedCollection: CollectionSlug
  where: Where
  columns?: Array<{
    accessor: string
    active: boolean
  }>
  access: {
    read: {
      constraint: 'everyone' | 'onlyMe' | 'specificUsers' | string
      users?: string[]
    }
    update: {
      constraint: 'everyone' | 'onlyMe' | 'specificUsers' | string  
      users?: string[]
    }
    delete: {
      constraint: 'everyone' | 'onlyMe' | 'specificUsers' | string
      users?: string[]
    }
  }
}

// Custom constraint definition
interface QueryPresetConstraint {
  label: string
  value: string
  fields?: Field[]
  access: Access<QueryPreset>
}
```

## Usage Guides

### Setting Up Role-Based Query Presets

Configure query presets with role-based access control for different organizational needs:

```typescript
import type { Config } from 'payload'

export const config: Config = {
  collections: [
    {
      slug: 'articles',
      enableQueryPresets: true,
      fields: [
        { name: 'title', type: 'text' },
        { name: 'status', type: 'select', options: ['draft', 'review', 'published'] },
        { name: 'author', type: 'relationship', relationTo: 'users' },
        { name: 'category', type: 'relationship', relationTo: 'categories' }
      ]
    }
  ],
  queryPresets: {
    // Collection-level access: Only editors and admins can manage presets
    access: {
      create: ({ req }) => ['editor', 'admin'].includes(req.user?.role),
      read: ({ req }) => Boolean(req.user),
      update: ({ req }) => ['editor', 'admin'].includes(req.user?.role),
      delete: ({ req }) => req.user?.role === 'admin'
    },
    
    // Custom constraints for different sharing levels
    constraints: {
      read: [
        {
          label: 'Team Members',
          value: 'teamMembers',
          fields: [
            {
              name: 'teams',
              type: 'relationship',
              relationTo: 'teams',
              hasMany: true
            }
          ],
          access: ({ req }) => ({
            'access.read.teams': {
              in: req.user?.teams || []
            }
          })
        },
        {
          label: 'Role-Based',
          value: 'roleBased', 
          fields: [
            {
              name: 'roles',
              type: 'select',
              hasMany: true,
              options: [
                { label: 'Writer', value: 'writer' },
                { label: 'Editor', value: 'editor' },
                { label: 'Admin', value: 'admin' }
              ]
            }
          ],
          access: ({ req }) => ({
            'access.read.roles': {
              in: [req.user?.role]
            }
          })
        }
      ]
    },
    
    // Restrict certain constraints based on user role
    filterConstraints: ({ req, options }) => {
      const userRole = req.user?.role
      
      // Only admins can create "everyone" presets
      if (userRole !== 'admin') {
        options = options.filter(option => 
          (typeof option === 'string' ? option : option.value) !== 'everyone'
        )
      }
      
      // Only editors and admins can use team-based sharing
      if (!['editor', 'admin'].includes(userRole)) {
        options = options.filter(option =>
          (typeof option === 'string' ? option : option.value) !== 'teamMembers'
        )
      }
      
      return options
    }
  }
}
```

### Creating Department-Specific Presets

Set up presets that are automatically scoped to user departments:

```typescript
import type { Config } from 'payload'

export const config: Config = {
  queryPresets: {
    constraints: {
      read: [
        {
          label: 'Department Only',
          value: 'departmentOnly',
          fields: [
            {
              name: 'department',
              type: 'text',
              admin: {
                readOnly: true,
                description: 'Automatically set based on your department'
              }
            }
          ],
          access: ({ req }) => {
            const userDepartment = req.user?.department
            return userDepartment ? {
              'access.read.department': {
                equals: userDepartment
              }
            } : false
          }
        },
        {
          label: 'Cross-Department',
          value: 'crossDepartment',
          fields: [
            {
              name: 'allowedDepartments',
              type: 'select',
              hasMany: true,
              options: [
                { label: 'Engineering', value: 'engineering' },
                { label: 'Marketing', value: 'marketing' },
                { label: 'Sales', value: 'sales' },
                { label: 'Support', value: 'support' }
              ]
            }
          ],
          access: ({ req }) => ({
            'access.read.allowedDepartments': {
              in: [req.user?.department]
            }
          })
        }
      ]
    }
  }
}
```

### Advanced Patterns

#### Time-Based Access Control

Create presets with time-based access restrictions:

```typescript
queryPresets: {
  constraints: {
    read: [
      {
        label: 'Time-Limited Access',
        value: 'timeLimited',
        fields: [
          {
            name: 'accessStartDate',
            type: 'date',
            admin: {
              date: {
                pickerAppearance: 'dayAndTime'
              }
            }
          },
          {
            name: 'accessEndDate', 
            type: 'date',
            admin: {
              date: {
                pickerAppearance: 'dayAndTime'
              }
            }
          }
        ],
        access: ({ req }) => {
          const now = new Date()
          return {
            and: [
              {
                'access.read.accessStartDate': {
                  less_than_equal: now.toISOString()
                }
              },
              {
                'access.read.accessEndDate': {
                  greater_than: now.toISOString()
                }
              }
            ]
          }
        }
      }
    ]
  }
}
```

#### Project-Based Preset Sharing

Configure presets that can be shared within specific projects:

```typescript
queryPresets: {
  constraints: {
    read: [
      {
        label: 'Project Team',
        value: 'projectTeam',
        fields: [
          {
            name: 'projects',
            type: 'relationship',
            relationTo: 'projects',
            hasMany: true,
            admin: {
              description: 'Users with access to these projects can use this preset'
            }
          }
        ],
        access: ({ req }) => {
          const userProjects = req.user?.projects || []
          return {
            'access.read.projects': {
              in: userProjects
            }
          }
        }
      }
    ]
  }
}
```

## API Reference

### Constants

#### `queryPresetsCollectionSlug`

- **Value**: `'payload-query-presets'`
- **Description**: The slug of the internal collection used to store query presets

```typescript
import { queryPresetsCollectionSlug } from 'payload'

console.log(queryPresetsCollectionSlug) // 'payload-query-presets'
```

#### `operations`

- **Value**: `['read', 'update', 'delete']`
- **Description**: Array of operations that can have access control constraints

```typescript
import { operations } from 'payload'

console.log(operations) // ['read', 'update', 'delete']
```

### Functions

#### `getQueryPresetsConfig(config: Config)`

Creates the internal collection configuration for query presets.

**Parameters:**
| Parameter | Type | Description |
|-----------|------|-------------|
| `config` | `Config` | The main PayloadCMS configuration object |

**Returns:** `CollectionConfig`

**Example:**
```typescript
import { getQueryPresetsConfig } from 'payload'
import type { Config } from 'payload'

const config: Config = {
  collections: [/* your collections */],
  queryPresets: {/* your preset config */}
}

const presetsCollection = getQueryPresetsConfig(config)
// Returns complete collection configuration for query presets
```

#### `getAccess(config: Config)`

Generates access control functions for the query presets collection.

**Parameters:**
| Parameter | Type | Description |
|-----------|------|-------------|
| `config` | `Config` | The main PayloadCMS configuration object |

**Returns:** `Record<Operation, Access>`

#### `getConstraints(config: Config)`

Creates the access control constraint fields for the query presets form.

**Parameters:**
| Parameter | Type | Description |
|-----------|------|-------------|
| `config` | `Config` | The main PayloadCMS configuration object |

**Returns:** `Field`

#### `preventLockout`

Validation function that prevents users from accidentally removing their own access to presets.

**Type:** `Validate`

**Description:** Creates a temporary preset record to validate that the user would still have access after the proposed changes, preventing accidental lockouts.

### TypeScript Types

```typescript
// Core query preset structure
interface QueryPreset {
  id: string | number
  title: string
  isShared: boolean
  relatedCollection: CollectionSlug
  where: Where
  columns?: Array<{
    accessor: string
    active: boolean
  }>
  access: {
    [operation in ConstraintOperation]: {
      constraint: DefaultConstraint
      users?: string[]
      // Additional custom constraint fields
      [key: string]: any
    }
  }
}

// Access constraint definition  
interface QueryPresetConstraint {
  label: string
  value: string
  fields?: Field[]
  access: Access<QueryPreset>
}

// Operation types
type ConstraintOperation = 'read' | 'update' | 'delete'
type DefaultConstraint = 'everyone' | 'onlyMe' | 'specificUsers'
type Constraint = DefaultConstraint | string

// Configuration types
type QueryPresetConstraints = QueryPresetConstraint[]
```

## Integrations

### Admin Interface Integration

The query presets system integrates seamlessly with PayloadCMS admin components:

- **Collection List Views**: Preset controls appear in collection list views when enabled
- **Filter Management**: Saved presets can include complex filter configurations
- **Column Configuration**: Presets remember which columns are visible and their order
- **Sorting Preferences**: Sort order is preserved within presets
- **Access Control UI**: Visual interface for managing preset sharing and permissions

### Database Integration

The system creates and manages the `payload-query-presets` collection:

- **Schema**: Automatically configured with proper relationships and validation
- **Access Control**: Multi-level access control with both static and dynamic rules
- **Indexes**: Optimized queries with indexes on related collections and access fields
- **Validation**: Built-in validation for JSON structures and access configurations

### Collection Integration

Query presets integrate with existing collections:

- **EnableQueryPresets**: Simple boolean flag to enable preset functionality
- **Automatic Relationships**: Presets automatically reference enabled collections
- **Field Integration**: Works with all PayloadCMS field types for filtering
- **Permission Integration**: Respects existing collection-level access control

## Troubleshooting

### Common Issues

#### Presets Not Appearing

**Problem:** Query presets are not showing in the admin interface for a collection.

**Solution:**
1. Verify `enableQueryPresets: true` is set on the collection
2. Ensure the user has read access to the query presets collection
3. Check that the collection is included in the query presets configuration

**Example:**
```typescript
// ❌ Wrong - presets not enabled
export const Posts: CollectionConfig = {
  slug: 'posts',
  // Missing: enableQueryPresets: true
  fields: [/* ... */]
}

// ✅ Correct - presets enabled
export const Posts: CollectionConfig = {
  slug: 'posts',
  enableQueryPresets: true, // Enable presets
  fields: [/* ... */]
}
```

#### Access Lockout Prevention

**Problem:** Users are getting locked out of their own presets when updating access control.

**Solution:**
The system includes automatic lockout prevention, but ensure you understand the rules:

**Example:**
```typescript
// The system automatically prevents this scenario:
// 1. User creates preset with "onlyMe" access
// 2. User tries to change to "specificUsers" without including themselves
// 3. System throws error: "This action will lock you out of this preset"

// Proper update flow
const preset = {
  title: 'My Preset',
  access: {
    read: {
      constraint: 'specificUsers',
      users: [currentUser.id, 'other-user-id'] // Always include current user
    }
  }
}
```

#### Invalid JSON in Where Clauses

**Problem:** Getting validation errors when saving complex filter conditions.

**Solution:**
Ensure filter conditions are properly formatted for the database adapter:

**Example:**
```typescript
// ❌ Wrong - client-side format
const invalidWhere = {
  title: { contains: 'test' }, // Client format
  status: { in: ['published'] }
}

// ✅ Correct - server-side format  
const validWhere = {
  title: { contains: 'test' },
  status: { in: ['published'] }
} // System automatically transforms this
```

#### Custom Constraints Not Working

**Problem:** Custom constraint fields are not appearing or access rules aren't working.

**Solution:**
Verify constraint configuration includes all required properties:

**Example:**
```typescript
// ❌ Wrong - missing required properties
{
  label: 'Custom Constraint',
  // Missing: value property
  access: ({ req }) => ({ /* access rules */ })
}

// ✅ Correct - complete constraint configuration
{
  label: 'Custom Constraint',
  value: 'customConstraint', // Required unique identifier
  fields: [
    {
      name: 'customField',
      type: 'text'
    }
  ],
  access: ({ req }) => ({
    'access.read.customField': {
      equals: req.user?.customProperty
    }
  })
}
```

### Debugging

Enable debug logging to troubleshoot query preset issues:

```typescript
export const config: Config = {
  queryPresets: {
    access: {
      read: ({ req }) => {
        console.log('Query preset read access check:', {
          user: req.user?.id,
          role: req.user?.role
        })
        return Boolean(req.user)
      }
    }
  }
}
```

Monitor query preset collection directly:

```typescript
// Check current presets
const debugPresets = async (payload: Payload) => {
  const presets = await payload.find({
    collection: 'payload-query-presets',
    depth: 2
  })
  
  console.log(`Found ${presets.totalDocs} query presets:`)
  presets.docs.forEach(preset => {
    console.log(`- ${preset.title} (${preset.relatedCollection})`)
    console.log(`  Access:`, preset.access)
    console.log(`  Shared:`, preset.isShared)
  })
  
  return presets
}
```

## Performance

### Performance Optimization

1. **Index Strategy**: The system automatically creates indexes on frequently queried fields
2. **Access Control Caching**: Consider caching access control results for complex constraints
3. **Preset Cleanup**: Regularly clean up unused or obsolete presets
4. **Query Optimization**: Ensure custom constraint access functions are efficient

```typescript
// Optimize custom constraints with caching
const roleCache = new Map()

queryPresets: {
  constraints: {
    read: [
      {
        label: 'Cached Role Check',
        value: 'cachedRole',
        access: ({ req }) => {
          const userId = req.user?.id
          const cacheKey = `user-${userId}-roles`
          
          if (!roleCache.has(cacheKey)) {
            // Expensive role lookup
            const userRoles = expensiveRoleQuery(userId)
            roleCache.set(cacheKey, userRoles, { ttl: 300000 }) // 5 minutes
          }
          
          const roles = roleCache.get(cacheKey)
          return {
            'access.read.allowedRoles': {
              in: roles
            }
          }
        }
      }
    ]
  }
}
```

## Security

### Security Considerations

1. **Access Control Validation**: All access control rules are validated server-side
2. **Lockout Prevention**: Automatic prevention of accidental access removal
3. **Input Sanitization**: All query inputs are validated and sanitized
4. **Privilege Escalation**: Custom constraints cannot bypass collection-level access control

```typescript
// Secure custom constraint implementation
queryPresets: {
  constraints: {
    read: [
      {
        label: 'Secure Department Access',
        value: 'secureDepartment',
        fields: [
          {
            name: 'department',
            type: 'select',
            options: [/* department options */],
            validate: (value, { req }) => {
              // Validate user can only select their own department
              if (value && value !== req.user?.department) {
                return 'You can only create presets for your own department'
              }
              return true
            }
          }
        ],
        access: ({ req }) => {
          // Double-check access server-side
          const userDepartment = req.user?.department
          if (!userDepartment) return false
          
          return {
            'access.read.department': {
              equals: userDepartment
            }
          }
        }
      }
    ]
  }
}
```

## Migration

### Migrating Query Preset Configurations

When updating query preset configurations, handle existing presets gracefully:

```typescript
// Migration helper for constraint changes
const migrateQueryPresets = async (payload: Payload) => {
  const presets = await payload.find({
    collection: 'payload-query-presets',
    limit: 1000
  })
  
  for (const preset of presets.docs) {
    let needsUpdate = false
    const updatedAccess = { ...preset.access }
    
    // Migrate old constraint format to new format
    Object.keys(updatedAccess).forEach(operation => {
      if (updatedAccess[operation].constraint === 'oldConstraintValue') {
        updatedAccess[operation].constraint = 'newConstraintValue'
        needsUpdate = true
      }
    })
    
    if (needsUpdate) {
      await payload.update({
        collection: 'payload-query-presets',
        id: preset.id,
        data: {
          access: updatedAccess
        }
      })
    }
  }
}
```

## Contributing

Found a bug or have a suggestion? [Open an issue](https://github.com/payloadcms/payload/issues) or submit a Pull Request.

## License

MIT License - see the [LICENSE](https://github.com/payloadcms/payload/blob/main/LICENSE) file for details.