# PayloadCMS Folders System Documentation

## Overview

The PayloadCMS Folders system provides hierarchical organization for documents within collections, enabling users to organize content into nested folder structures. This system creates a virtual file system-like interface for managing documents across multiple collections with support for collection-specific scoping, breadcrumb navigation, and drag-and-drop organization.

## Key Features

- **Hierarchical Organization**: Create nested folder structures to organize documents
- **Collection-Specific Folders**: Scope folders to specific collections or make them collection-agnostic  
- **Browse by Folder View**: Visual interface for navigating folder structures
- **Automatic Field Injection**: Seamlessly adds folder fields to existing collections
- **Validation System**: Ensures proper folder-document relationships and permissions
- **Hook System**: Comprehensive lifecycle hooks for folder operations
- **Breadcrumb Navigation**: Dynamic breadcrumb generation for folder paths

## System Requirements

### Dependencies
- Node.js 18+ or compatible runtime
- PayloadCMS core system
- Database adapter (MongoDB, PostgreSQL, etc.)
- React Server Components support

### Required Imports
```typescript
import type { 
  FolderInterface, 
  RootFoldersConfiguration, 
  CollectionFoldersConfiguration 
} from './src/folders/types.js'
```

## Installation

The folders system is built into PayloadCMS core. Enable it in your config:

```typescript
import { buildConfig } from 'payload/config'

export default buildConfig({
  folders: {
    slug: 'folders',
    fieldName: 'folder',
    browseByFolder: true,
    collectionSpecific: true,
    debug: false
  },
  collections: [
    {
      slug: 'posts',
      folders: {
        browseByFolder: true
      },
      fields: [
        // Folder field is automatically added
        { name: 'title', type: 'text' }
      ]
    }
  ]
})
```

## Configuration

### Root Folders Configuration

```typescript
type RootFoldersConfiguration = {
  browseByFolder?: boolean      // Enable browse by folder view (default: true)
  collectionSpecific?: boolean  // Enable collection scoping (default: true)
  debug?: boolean              // Show hidden folder fields (default: false)
  fieldName?: string           // Folder field name (default: "folder")
  slug?: string               // Folder collection slug (default: "payload-folders")
  collectionOverrides?: Array<(args: { collection: CollectionConfig }) => CollectionConfig>
}
```

### Collection Folders Configuration

```typescript
type CollectionFoldersConfiguration = {
  browseByFolder?: boolean  // Include in browse by folder view (default: true)
}
```

## Core Components

### 1. Folder Collection Creation

```typescript
// createFolderCollection.ts
export const createFolderCollection = ({
  slug,
  collectionSpecific,
  debug,
  folderEnabledCollections,
  folderFieldName,
}: CreateFolderCollectionArgs): CollectionConfig => {
  return {
    slug,
    access: { /* defaultAccess for all operations */ },
    admin: {
      hidden: !debug,
      useAsTitle: 'name'
    },
    fields: [
      { name: 'name', type: 'text', required: true },
      buildFolderField({ /* folder relationship field */ }),
      { name: 'documentsAndFolders', type: 'join' },
      // Collection-specific folder type selection if enabled
    ],
    hooks: {
      afterChange: [reparentChildFolder],
      afterDelete: [dissasociateAfterDelete],
      beforeDelete: [deleteSubfoldersBeforeDelete],
      beforeValidate: [ensureSafeCollectionsChange]
    }
  }
}
```

### 2. Folder Field Builder

```typescript
// buildFolderField.ts
export const buildFolderField = ({
  collectionSpecific,
  folderFieldName,
  folderSlug,
  overrides = {}
}: BuildFolderFieldArgs): SingleRelationshipField => {
  return {
    name: folderFieldName,
    type: 'relationship',
    relationTo: folderSlug,
    validate: async (value, context) => {
      // Validation logic for collection-specific folders
      // Ensures folders accept the correct document types
    }
  }
}
```

### 3. Folder Data Retrieval

```typescript
// getFolderData.ts
export const getFolderData = async ({
  collectionSlug,
  documentWhere,
  folderID,
  folderWhere,
  req,
  sort = 'name'
}: GetFolderDataArgs): Promise<GetFolderDataResult> => {
  // Returns documents, subfolders, breadcrumbs, and folder assignments
  return {
    breadcrumbs: FolderBreadcrumb[],
    documents: FolderOrDocument[],
    folderAssignedCollections: CollectionSlug[],
    subfolders: FolderOrDocument[]
  }
}
```

## TypeScript Interfaces

### Core Types

```typescript
// Folder document structure
export type FolderInterface = {
  documentsAndFolders?: {
    docs: {
      relationTo: CollectionSlug
      value: Document
    }[]
  }
  folder?: FolderInterface | (number | string | undefined)
  folderType: CollectionSlug[]  // Collection scoping
  name: string
} & TypeWithID

// Breadcrumb navigation
export type FolderBreadcrumb = {
  folderType?: CollectionSlug[]
  id: null | number | string
  name: string
}

// Generic folder or document item
export type FolderOrDocument = {
  itemKey: FolderDocumentItemKey
  relationTo: CollectionSlug
  value: {
    _folderOrDocumentTitle: string
    createdAt?: string
    folderID?: number | string
    folderType: CollectionSlug[]
    id: number | string
    updatedAt?: string
    // Media data for upload collections
    filename?: string
    mimeType?: string
    url?: string
  }
}
```

### Hook System

```typescript
// Lifecycle hooks for folder operations
export const deleteSubfoldersBeforeDelete: CollectionBeforeDeleteHook
export const dissasociateAfterDelete: CollectionAfterDeleteHook  
export const ensureSafeCollectionsChange: CollectionBeforeValidateHook
export const reparentChildFolder: CollectionAfterChangeHook
```

## Usage Examples

### Basic Folder Setup

```typescript
// Enable folders for a collection
export const Posts: CollectionConfig = {
  slug: 'posts',
  folders: {
    browseByFolder: true
  },
  fields: [
    { name: 'title', type: 'text' },
    { name: 'content', type: 'richText' }
    // 'folder' field automatically added
  ]
}
```

### Collection-Specific Folders

```typescript
// Create folders that only accept certain collection types
const createNewsFolder = async (req: PayloadRequest) => {
  const folder = await req.payload.create({
    collection: 'payload-folders',
    data: {
      name: 'News Articles',
      folderType: ['posts', 'articles']  // Only accepts these types
    }
  })
  return folder
}
```

### Querying Folder Contents

```typescript
// Get all documents and subfolders in a specific folder
const folderData = await getFolderData({
  folderID: 'folder-123',
  collectionSlug: 'posts',  // Optional: filter by collection
  sort: '-createdAt',       // Sort by creation date descending
  req,
  documentWhere: {         // Optional document filtering
    status: { equals: 'published' }
  },
  folderWhere: {          // Optional folder filtering
    name: { contains: 'Archive' }
  }
})

// Access results
const { documents, subfolders, breadcrumbs, folderAssignedCollections } = folderData
```

### Creating Nested Folder Structure

```typescript
// Create parent folder
const parentFolder = await req.payload.create({
  collection: 'payload-folders',
  data: {
    name: 'Content',
    folderType: ['posts', 'pages']
  }
})

// Create child folder
const childFolder = await req.payload.create({
  collection: 'payload-folders',
  data: {
    name: 'Blog Posts',
    folder: parentFolder.id,
    folderType: ['posts']  // More restrictive than parent
  }
})
```

### Moving Documents Between Folders

```typescript
// Move document to different folder
await req.payload.update({
  collection: 'posts',
  id: 'post-123',
  data: {
    folder: 'new-folder-id'
  }
})

// Move to root level (no folder)
await req.payload.update({
  collection: 'posts',
  id: 'post-123',
  data: {
    folder: null
  }
})
```

## Hooks and Validation

### Folder Validation

The system includes comprehensive validation:

```typescript
// Validates folder-document relationships
const validateFolderAssignment = async (value, context) => {
  if (!collectionSpecific || !value) return true
  
  const parentFolder = await req.payload.findByID({
    id: value,
    collection: folderSlug,
    select: { folderType: true }
  })
  
  const allowedTypes = parentFolder.folderType || []
  if (allowedTypes.length === 0) return true  // Accepts all types
  
  if (!allowedTypes.includes(context.collectionSlug)) {
    return `Folder does not allow documents of type ${context.collectionSlug}`
  }
  
  return true
}
```

### Lifecycle Hooks

```typescript
// Auto-delete subfolders when parent is deleted
const deleteSubfoldersBeforeDelete: CollectionBeforeDeleteHook = ({ id, req }) => {
  return req.payload.delete({
    collection: folderSlug,
    where: { folder: { equals: id } }
  })
}

// Dissociate documents from deleted folders
const dissasociateAfterDelete: CollectionAfterDeleteHook = ({ id, req }) => {
  // Remove folder references from all affected documents
}

// Reparent child folders when parent changes
const reparentChildFolder: CollectionAfterChangeHook = ({ doc, req }) => {
  // Update child folder relationships
}
```

## Utilities

### Folder Constraints

```typescript
// buildFolderWhereConstraints.ts
export const buildFolderWhereConstraints = (args: ConstraintArgs): Where => {
  // Build where clauses for folder queries
  return {
    and: [
      { folder: { equals: folderID } },
      { collection: { in: allowedCollections } }
    ]
  }
}
```

### Document Formatting

```typescript
// formatFolderOrDocumentItem.ts
export const formatFolderOrDocumentItem = (
  doc: Document,
  collection: SanitizedCollectionConfig
): FolderOrDocument => {
  return {
    itemKey: `${collection.slug}-${doc.id}`,
    relationTo: collection.slug,
    value: {
      id: doc.id,
      _folderOrDocumentTitle: getDocumentTitle(doc, collection),
      folderType: doc.folderType || [],
      createdAt: doc.createdAt,
      updatedAt: doc.updatedAt,
      // Additional media data for uploads
      ...(collection.upload && {
        filename: doc.filename,
        mimeType: doc.mimeType,
        url: doc.url
      })
    }
  }
}
```

### Breadcrumb Generation

```typescript
// getFolderBreadcrumbs.ts
export const getFolderBreadcrumbs = async ({
  folderID,
  req
}: BreadcrumbArgs): Promise<FolderBreadcrumb[]> => {
  const breadcrumbs: FolderBreadcrumb[] = []
  let currentFolderID = folderID
  
  while (currentFolderID) {
    const folder = await req.payload.findByID({
      id: currentFolderID,
      collection: req.payload.config.folders.slug
    })
    
    breadcrumbs.unshift({
      id: folder.id,
      name: folder.name,
      folderType: folder.folderType
    })
    
    currentFolderID = folder.folder?.id
  }
  
  // Add root breadcrumb
  breadcrumbs.unshift({
    id: null,
    name: 'Root',
    folderType: undefined
  })
  
  return breadcrumbs
}
```

## API Integration

### REST API Endpoints

```typescript
// GET /api/folders - List all folders
// GET /api/folders/:id - Get specific folder
// POST /api/folders - Create new folder
// PATCH /api/folders/:id - Update folder
// DELETE /api/folders/:id - Delete folder

// Folder-specific endpoints
// GET /api/folders/:id/contents - Get folder contents
// GET /api/folders/:id/breadcrumbs - Get folder breadcrumbs
```

### GraphQL Queries

```graphql
# Query folder with contents
query GetFolder($id: String!) {
  Folder(id: $id) {
    id
    name
    folderType
    folder {
      id
      name
    }
    documentsAndFolders {
      docs {
        relationTo
        value {
          ... on Post {
            id
            title
          }
        }
      }
    }
  }
}

# Query folder breadcrumbs
query GetFolderBreadcrumbs($id: String!) {
  Folder(id: $id) {
    id
    name
    folder {
      id
      name
      folder {
        id
        name
      }
    }
  }
}
```

## Admin Interface Integration

### Browse by Folder View

The system integrates with the PayloadCMS admin interface to provide:

- Visual folder navigation with drag-and-drop
- Breadcrumb navigation bars
- Collection filtering in folder views
- Document cards with folder context
- Nested folder creation and management

### Customization

```typescript
// Custom folder field components
export const CustomFolderField: React.FC<FolderFieldProps> = (props) => {
  return (
    <div className="folder-field">
      {/* Custom folder selection interface */}
    </div>
  )
}

// Register custom field
fields: [{
  name: 'folder',
  type: 'relationship',
  relationTo: 'payload-folders',
  admin: {
    components: {
      Field: CustomFolderField
    }
  }
}]
```

## Performance Considerations

### Database Indexing

```typescript
// Recommended indexes for folder performance
{
  name: 'folder',
  type: 'relationship',
  index: true,  // Index for folder queries
  relationTo: 'payload-folders'
}

// Compound indexes for complex queries
db.posts.createIndex({ folder: 1, status: 1, createdAt: -1 })
db.folders.createIndex({ folder: 1, folderType: 1 })
```

### Caching Strategies

```typescript
// Cache folder data for performance
const cachedFolderData = await cache.get(`folder:${folderID}`)
if (!cachedFolderData) {
  const folderData = await getFolderData({ folderID, req })
  await cache.set(`folder:${folderID}`, folderData, 300) // 5 min cache
}
```

### Query Optimization

```typescript
// Optimize folder queries with selective field loading
const optimizedQuery = await req.payload.find({
  collection: 'payload-folders',
  where: { folder: { equals: parentID } },
  select: {
    id: true,
    name: true,
    folderType: true
    // Exclude heavy fields like documentsAndFolders
  },
  limit: 100
})
```

## Troubleshooting

### Common Issues

**Folder validation errors:**
```typescript
// Check folder type compatibility
const validateFolderTypes = (parentTypes: string[], documentType: string) => {
  if (parentTypes.length === 0) return true  // Accepts all
  return parentTypes.includes(documentType)
}
```

**Orphaned documents after folder deletion:**
```typescript
// Find documents without valid folder references
const orphanedDocs = await req.payload.find({
  collection: 'posts',
  where: {
    and: [
      { folder: { exists: true } },
      { folder: { not_in: validFolderIDs } }
    ]
  }
})
```

**Performance issues with deep nesting:**
```typescript
// Limit folder depth to prevent performance issues
const MAX_FOLDER_DEPTH = 10

const validateFolderDepth = async (folderID: string, depth = 0) => {
  if (depth > MAX_FOLDER_DEPTH) {
    throw new Error('Maximum folder depth exceeded')
  }
  
  const folder = await req.payload.findByID({
    id: folderID,
    collection: 'payload-folders'
  })
  
  if (folder.folder) {
    return validateFolderDepth(folder.folder.id, depth + 1)
  }
  
  return depth
}
```

**Collection-specific folder issues:**
```typescript
// Debug folder type assignments
const debugFolderTypes = async (folderID: string) => {
  const folder = await req.payload.findByID({
    id: folderID,
    collection: 'payload-folders',
    select: { folderType: true, name: true }
  })
  
  console.log(`Folder "${folder.name}" accepts:`, folder.folderType || 'All collections')
}
```

### Debugging

Enable debug mode to see hidden folder fields:

```typescript
export default buildConfig({
  folders: {
    debug: true  // Shows internal folder fields in admin
  }
})
```

## Security Considerations

### Access Control

```typescript
// Folder-aware access control
const folderAwareAccess = async ({ req, data }) => {
  if (data.folder) {
    const folder = await req.payload.findByID({
      id: data.folder,
      collection: 'payload-folders'
    })
    
    // Check if user has access to parent folder
    return checkFolderAccess(folder, req.user)
  }
  
  return defaultAccess({ req, data })
}
```

### Data Validation

```typescript
// Prevent circular folder references
const preventCircularReference = async (folderID: string, parentID: string) => {
  let currentID = parentID
  const visited = new Set()
  
  while (currentID && !visited.has(currentID)) {
    if (currentID === folderID) {
      throw new Error('Circular folder reference detected')
    }
    
    visited.add(currentID)
    const folder = await req.payload.findByID({
      id: currentID,
      collection: 'payload-folders'
    })
    currentID = folder.folder?.id
  }
}
```

## Related Documentation

- [Collections Documentation](./collections/README-extended.md) - Document management system
- [Fields Documentation](./fields/README-extended.md) - Field types and validation
- [Admin Documentation](./admin/README-extended.md) - Admin interface integration
- [Auth Documentation](./auth/README-extended.md) - Access control and permissions

## Version Compatibility

- PayloadCMS 3.0+ - Full folders system support
- PayloadCMS 2.x - Limited folder functionality
- React 18+ - Required for admin interface components
- Node.js 18+ - Required for proper TypeScript support

---

*This documentation covers PayloadCMS Folders System v3.0+. For older versions, refer to the legacy documentation.*