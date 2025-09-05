---
title: PayloadCMS Collections System
label: Collections
order: 5
desc: Complete collection management system with CRUD operations, hooks, access control, versioning, file uploads, and database abstractions
keywords: [collections, crud, operations, hooks, access-control, versioning, database, api, endpoints, documents]
---

![NPM Version](https://img.shields.io/npm/v/payload)
![Bundle Size](https://img.shields.io/bundlephobia/minzip/payload)

## Overview

The PayloadCMS Collections System is the core data management layer that provides comprehensive CRUD (Create, Read, Update, Delete) operations for structured content. Collections are the primary building blocks for storing and managing data in PayloadCMS, offering a rich set of features including sophisticated hooks system, fine-grained access control, versioning, file uploads, and database abstractions that work across multiple database adapters.

This system is designed for enterprise applications requiring complex data operations with full type safety, extensive customization capabilities, and high-performance database queries. It provides both REST and GraphQL APIs out of the box, comprehensive hook system for business logic integration, and powerful access control mechanisms that can handle the most complex authorization requirements.

The collections system abstracts away database-specific implementations while providing advanced features like transactions, joins, indexing, and query optimization across MongoDB, PostgreSQL, and other supported databases.

<Banner type="info">
The package is open-source. [View source code](https://github.com/payloadcms/payload/tree/main/packages/payload/src/collections). Need help? [Community Help](https://payloadcms.com/community-help).
</Banner>

## System Requirements

- **PayloadCMS**: ^3.54.0
- **Node.js**: ^18.20.2 || >=20.9.0
- **TypeScript**: ^5.0.0 (recommended)
- **Database**: MongoDB, PostgreSQL, SQLite, or other supported adapters

## Key Features

- 🔧 **Complete CRUD Operations** - Create, read, update, delete with full transaction support
- 🎣 **Comprehensive Hook System** - Before/after hooks for all operations with async support
- 🔒 **Advanced Access Control** - Field-level and document-level permissions with complex rules
- 📝 **Document Versioning** - Track changes, drafts, and publish workflows
- 📁 **File Upload Management** - Built-in file handling with image processing
- 🗃️ **Database Abstraction** - Works with multiple database types transparently
- ⚡ **Performance Optimized** - Query optimization, caching, and efficient data loading
- 🌍 **Internationalization** - Multi-locale content management
- 🔍 **Advanced Querying** - Complex where clauses, joins, and sorting
- 📊 **Real-time Updates** - Live preview and collaborative editing support

## Architecture Overview

The collections system is built on several key architectural layers:

### Configuration Layer
- **Collection Config**: Defines collection structure, fields, and behavior
- **Field Definitions**: Specifies data types, validation, and relationships
- **Access Patterns**: Configures permissions and access control rules

### Operation Layer
- **CRUD Operations**: Core create, read, update, delete functionality
- **Hook System**: Extensible before/after operation hooks
- **Validation**: Server-side data validation and sanitization

### Database Layer
- **Adapter Pattern**: Database-agnostic operations
- **Query Building**: Optimized query generation
- **Transaction Management**: ACID compliance and rollback support

### API Layer
- **REST Endpoints**: Auto-generated RESTful API
- **GraphQL Schema**: Dynamic GraphQL API generation
- **Webhook Support**: External system integration

## Configuration

### Basic Collection Setup

```typescript
import { CollectionConfig } from 'payload'

const Posts: CollectionConfig = {
  slug: 'posts',
  
  // Fields define the data structure
  fields: [
    {
      name: 'title',
      type: 'text',
      required: true,
    },
    {
      name: 'content',
      type: 'richText',
    },
    {
      name: 'status',
      type: 'select',
      options: [
        { label: 'Draft', value: 'draft' },
        { label: 'Published', value: 'published' },
        { label: 'Archived', value: 'archived' },
      ],
      defaultValue: 'draft',
    },
    {
      name: 'publishedAt',
      type: 'date',
      admin: {
        condition: (data) => data.status === 'published',
      },
    },
  ],
  
  // Admin interface configuration
  admin: {
    useAsTitle: 'title',
    defaultColumns: ['title', 'status', 'publishedAt', 'updatedAt'],
    group: 'Content',
  },
  
  // Enable timestamps
  timestamps: true,
}
```

### Advanced Collection Configuration

```typescript
import { CollectionConfig } from 'payload'

const Products: CollectionConfig = {
  slug: 'products',
  
  // Access control
  access: {
    read: ({ req: { user } }) => {
      // Public products are readable by everyone
      if (!user) return { status: { equals: 'published' } }
      
      // Admins can read everything
      if (user.role === 'admin') return true
      
      // Others can only read published products
      return { status: { equals: 'published' } }
    },
    
    create: ({ req: { user } }) => {
      return user?.role === 'admin' || user?.role === 'editor'
    },
    
    update: ({ req: { user } }) => {
      return user?.role === 'admin' || user?.role === 'editor'
    },
    
    delete: ({ req: { user } }) => {
      return user?.role === 'admin'
    },
  },
  
  // Hooks for business logic
  hooks: {
    beforeCreate: [
      ({ data, req }) => {
        // Auto-generate slug from title
        if (data.title && !data.slug) {
          data.slug = data.title
            .toLowerCase()
            .replace(/[^a-z0-9]+/g, '-')
            .replace(/^-+|-+$/g, '')
        }
        
        // Set created by user
        data.createdBy = req.user?.id
        
        return data
      },
    ],
    
    afterChange: [
      async ({ doc, previousDoc, operation, req }) => {
        // Send notification when status changes
        if (operation === 'update' && doc.status !== previousDoc?.status) {
          await req.payload.sendEmail({
            to: 'admin@company.com',
            subject: `Product ${doc.title} status changed`,
            html: `Product status changed from ${previousDoc?.status} to ${doc.status}`,
          })
        }
      },
    ],
    
    beforeDelete: [
      async ({ id, req }) => {
        // Check for dependencies before deletion
        const orders = await req.payload.find({
          collection: 'orders',
          where: {
            'products.product': { equals: id },
          },
          limit: 1,
        })
        
        if (orders.totalDocs > 0) {
          throw new Error('Cannot delete product that has orders')
        }
      },
    ],
  },
  
  fields: [
    {
      name: 'title',
      type: 'text',
      required: true,
      localized: true,
    },
    {
      name: 'slug',
      type: 'text',
      unique: true,
      index: true,
      admin: {
        position: 'sidebar',
      },
    },
    {
      name: 'description',
      type: 'richText',
      localized: true,
    },
    {
      name: 'price',
      type: 'number',
      required: true,
      min: 0,
      admin: {
        step: 0.01,
      },
    },
    {
      name: 'category',
      type: 'relationship',
      relationTo: 'categories',
      hasMany: false,
      required: true,
    },
    {
      name: 'tags',
      type: 'relationship',
      relationTo: 'tags',
      hasMany: true,
    },
    {
      name: 'images',
      type: 'array',
      fields: [
        {
          name: 'image',
          type: 'upload',
          relationTo: 'media',
          required: true,
        },
        {
          name: 'alt',
          type: 'text',
          required: true,
        },
      ],
      minRows: 1,
      maxRows: 10,
    },
    {
      name: 'variants',
      type: 'array',
      fields: [
        {
          name: 'name',
          type: 'text',
          required: true,
        },
        {
          name: 'sku',
          type: 'text',
          required: true,
          unique: true,
        },
        {
          name: 'price',
          type: 'number',
          required: true,
          min: 0,
        },
        {
          name: 'inventory',
          type: 'number',
          required: true,
          min: 0,
        },
      ],
    },
    {
      name: 'status',
      type: 'select',
      options: [
        { label: 'Draft', value: 'draft' },
        { label: 'Published', value: 'published' },
        { label: 'Out of Stock', value: 'out-of-stock' },
        { label: 'Discontinued', value: 'discontinued' },
      ],
      defaultValue: 'draft',
      admin: {
        position: 'sidebar',
      },
    },
    {
      name: 'featured',
      type: 'checkbox',
      defaultValue: false,
      admin: {
        position: 'sidebar',
      },
    },
    {
      name: 'seo',
      type: 'group',
      fields: [
        {
          name: 'title',
          type: 'text',
          maxLength: 60,
        },
        {
          name: 'description',
          type: 'textarea',
          maxLength: 160,
        },
        {
          name: 'keywords',
          type: 'text',
        },
      ],
    },
    {
      name: 'createdBy',
      type: 'relationship',
      relationTo: 'users',
      admin: {
        readOnly: true,
        position: 'sidebar',
      },
    },
  ],
  
  // Enable versioning and drafts
  versions: {
    maxPerDoc: 20,
    drafts: {
      autosave: {
        interval: 2000, // Auto-save every 2 seconds
      },
    },
  },
  
  // Database indexes for performance
  indexes: [
    {
      fields: ['status', 'featured'],
    },
    {
      fields: ['category', 'status'],
    },
    {
      unique: true,
      fields: ['slug'],
    },
  ],
  
  // Admin interface customization
  admin: {
    useAsTitle: 'title',
    defaultColumns: ['title', 'price', 'status', 'updatedAt'],
    group: 'E-commerce',
    listSearchableFields: ['title', 'description', 'slug'],
    preview: (doc) => `${process.env.WEBSITE_URL}/products/${doc.slug}`,
    
    // Custom components
    components: {
      views: {
        edit: {
          actions: ['/components/ProductActions'],
          tabs: [
            {
              label: 'Content',
              fields: ['title', 'description', 'images'],
            },
            {
              label: 'Pricing & Inventory',
              fields: ['price', 'variants'],
            },
            {
              label: 'SEO',
              fields: ['seo'],
            },
          ],
        },
      },
    },
  },
  
  // Custom API endpoints
  endpoints: [
    {
      path: '/featured',
      method: 'get',
      handler: async (req, res) => {
        const featuredProducts = await req.payload.find({
          collection: 'products',
          where: {
            and: [
              { featured: { equals: true } },
              { status: { equals: 'published' } },
            ],
          },
          limit: 10,
        })
        
        res.json(featuredProducts)
      },
    },
    {
      path: '/:id/reviews',
      method: 'get',
      handler: async (req, res) => {
        const reviews = await req.payload.find({
          collection: 'reviews',
          where: {
            product: { equals: req.params.id },
          },
        })
        
        res.json(reviews)
      },
    },
  ],
}
```

## CRUD Operations

### Create Operation

```typescript
// Server-side create operation
import { createOperation } from 'payload/collections'

// Direct operation call
const newProduct = await createOperation({
  collection: Products,
  data: {
    title: 'New Product',
    description: 'Product description',
    price: 29.99,
    status: 'draft',
    category: categoryId,
  },
  req,
})

// Using Payload instance
const newProduct = await payload.create({
  collection: 'products',
  data: {
    title: 'New Product',
    description: 'Product description', 
    price: 29.99,
    status: 'draft',
    category: categoryId,
  },
  user: req.user, // For access control
})

// Create with file upload
const productWithImage = await payload.create({
  collection: 'products',
  data: {
    title: 'Product with Image',
    images: [
      {
        image: uploadedFileId,
        alt: 'Product image',
      },
    ],
  },
  filesToUpload: [
    {
      file: uploadedFile,
      field: 'images.0.image',
    },
  ],
})

// Create with versioning
const product = await payload.create({
  collection: 'products',
  data: productData,
  draft: true, // Save as draft
  autosave: false, // Disable autosave
})

// Bulk create
const bulkResult = await payload.create({
  collection: 'products',
  data: [
    { title: 'Product 1', price: 10 },
    { title: 'Product 2', price: 20 },
    { title: 'Product 3', price: 30 },
  ],
})
```

### Read Operation

```typescript
// Find multiple documents
const products = await payload.find({
  collection: 'products',
  where: {
    and: [
      { status: { equals: 'published' } },
      { price: { greater_than: 10 } },
    ],
  },
  sort: '-createdAt',
  limit: 10,
  page: 1,
})

// Complex queries with relationships
const productsWithCategories = await payload.find({
  collection: 'products',
  where: {
    'category.name': { contains: 'Electronics' },
  },
  populate: {
    category: true,
    tags: true,
    images: {
      image: true,
    },
  },
  depth: 2,
})

// Find by ID
const product = await payload.findByID({
  collection: 'products',
  id: productId,
  populate: {
    category: true,
    createdBy: true,
  },
})

// Find with joins
const productsWithReviews = await payload.find({
  collection: 'products',
  joins: {
    reviews: {
      collection: 'reviews',
      on: 'product',
    },
  },
})

// Search and filtering
const searchResults = await payload.find({
  collection: 'products',
  where: {
    or: [
      { title: { contains: searchTerm } },
      { description: { contains: searchTerm } },
      { 'tags.name': { contains: searchTerm } },
    ],
  },
})

// Count documents
const productCount = await payload.count({
  collection: 'products',
  where: {
    status: { equals: 'published' },
  },
})

// Find distinct values
const categories = await payload.findDistinct({
  collection: 'products',
  field: 'category',
  where: {
    status: { equals: 'published' },
  },
})
```

### Update Operation

```typescript
// Update by ID
const updatedProduct = await payload.update({
  collection: 'products',
  id: productId,
  data: {
    title: 'Updated Product Title',
    price: 39.99,
  },
})

// Bulk update
const bulkUpdateResult = await payload.update({
  collection: 'products',
  where: {
    category: { equals: categoryId },
  },
  data: {
    status: 'published',
  },
})

// Update with file upload
const productWithNewImage = await payload.update({
  collection: 'products',
  id: productId,
  data: {
    images: [
      ...existingImages,
      {
        image: newImageId,
        alt: 'New image',
      },
    ],
  },
})

// Update with versioning
const publishedProduct = await payload.update({
  collection: 'products',
  id: productId,
  data: updatedData,
  draft: false, // Publish the changes
})

// Partial updates
const partialUpdate = await payload.update({
  collection: 'products',
  id: productId,
  data: {
    'seo.title': 'New SEO Title',
    'variants.0.price': 29.99,
  },
})
```

### Delete Operation

```typescript
// Delete by ID
await payload.delete({
  collection: 'products',
  id: productId,
})

// Bulk delete
const deleteResult = await payload.delete({
  collection: 'products',
  where: {
    status: { equals: 'draft' },
    createdAt: {
      less_than: new Date(Date.now() - 30 * 24 * 60 * 60 * 1000), // 30 days ago
    },
  },
})

// Soft delete (move to trash)
await payload.delete({
  collection: 'products',
  id: productId,
  trash: true, // Move to trash instead of permanent delete
})

// Restore from trash
await payload.update({
  collection: 'products',
  id: productId,
  data: {
    deletedAt: null,
  },
})
```

## Hook System

### Before Hooks

```typescript
const Collection: CollectionConfig = {
  slug: 'posts',
  
  hooks: {
    // Before validation
    beforeValidate: [
      ({ data, operation, originalDoc }) => {
        if (operation === 'create') {
          // Set default values
          data.author = data.author || req.user.id
          data.slug = data.slug || generateSlug(data.title)
        }
        
        return data
      },
    ],
    
    // Before change (after validation)
    beforeChange: [
      async ({ data, operation, originalDoc, req }) => {
        // Audit logging
        await req.payload.create({
          collection: 'audit-logs',
          data: {
            collection: 'posts',
            operation,
            documentId: originalDoc?.id || 'new',
            changes: data,
            user: req.user?.id,
          },
        })
        
        // Auto-generate excerpt
        if (data.content && !data.excerpt) {
          data.excerpt = stripHtml(data.content).substring(0, 150) + '...'
        }
        
        return data
      },
    ],
    
    // Before read
    beforeRead: [
      ({ doc, query, req }) => {
        // Track page views
        if (req.headers['x-track-views'] !== 'false') {
          payload.update({
            collection: 'posts',
            id: doc.id,
            data: {
              views: (doc.views || 0) + 1,
            },
          }).catch(() => {}) // Fire and forget
        }
        
        return doc
      },
    ],
    
    // Before delete
    beforeDelete: [
      async ({ id, req }) => {
        // Check for related content
        const relatedComments = await req.payload.count({
          collection: 'comments',
          where: { post: { equals: id } },
        })
        
        if (relatedComments.totalDocs > 0) {
          throw new Error(`Cannot delete post with ${relatedComments.totalDocs} comments`)
        }
      },
    ],
  },
}
```

### After Hooks

```typescript
const Collection: CollectionConfig = {
  slug: 'posts',
  
  hooks: {
    // After change
    afterChange: [
      async ({ doc, previousDoc, operation, req }) => {
        // Clear cache when content changes
        if (operation === 'update' && doc.status !== previousDoc?.status) {
          await req.payload.cache?.clear(`post-${doc.id}`)
        }
        
        // Send notifications
        if (doc.status === 'published' && previousDoc?.status !== 'published') {
          await sendNewPostNotification(doc, req)
        }
        
        // Update search index
        await updateSearchIndex('posts', doc)
      },
    ],
    
    // After read
    afterRead: [
      ({ doc, findMany, req }) => {
        // Add computed fields
        doc.readingTime = calculateReadingTime(doc.content)
        doc.isOwner = doc.author === req.user?.id
        
        // Add related data for single reads
        if (!findMany) {
          // This would be populated in another hook or middleware
          doc.relatedPosts = [] // Populated elsewhere
        }
        
        return doc
      },
    ],
    
    // After delete
    afterDelete: [
      async ({ doc, id, req }) => {
        // Clean up related data
        await req.payload.delete({
          collection: 'comments',
          where: { post: { equals: id } },
        })
        
        // Remove from search index
        await removeFromSearchIndex('posts', id)
        
        // Clear cache
        await req.payload.cache?.clear(`post-${id}`)
      },
    ],
  },
}
```

### Authentication Hooks

```typescript
const UsersCollection: CollectionConfig = {
  slug: 'users',
  auth: true,
  
  hooks: {
    // Before login
    beforeLogin: [
      ({ user }) => {
        if (!user.active) {
          throw new Error('Account is disabled')
        }
        
        // Update last login attempt
        user.lastLoginAttempt = new Date()
        
        return user
      },
    ],
    
    // After login
    afterLogin: [
      async ({ user, token, req }) => {
        // Track login
        await req.payload.create({
          collection: 'login-logs',
          data: {
            user: user.id,
            ip: req.ip,
            userAgent: req.headers['user-agent'],
            timestamp: new Date(),
          },
        })
        
        // Update user stats
        await req.payload.update({
          collection: 'users',
          id: user.id,
          data: {
            lastLogin: new Date(),
            loginCount: (user.loginCount || 0) + 1,
          },
        })
      },
    ],
    
    // After logout
    afterLogout: [
      async ({ user, req }) => {
        // Clear user sessions
        await req.payload.update({
          collection: 'users',
          id: user.id,
          data: {
            sessions: [],
          },
        })
      },
    ],
  },
}
```

## Access Control

### Field-Level Access Control

```typescript
const Collection: CollectionConfig = {
  slug: 'posts',
  
  fields: [
    {
      name: 'title',
      type: 'text',
      access: {
        read: () => true, // Everyone can read
        create: ({ req: { user } }) => Boolean(user), // Only authenticated users can create
        update: ({ req: { user }, doc }) => {
          // Only author or admin can update
          return user?.role === 'admin' || doc.author === user?.id
        },
      },
    },
    {
      name: 'salary',
      type: 'number',
      access: {
        read: ({ req: { user } }) => {
          // Only HR or the employee themselves can read salary
          return user?.role === 'hr' || user?.department === 'hr'
        },
        create: ({ req: { user } }) => user?.role === 'hr',
        update: ({ req: { user } }) => user?.role === 'hr',
      },
    },
    {
      name: 'internalNotes',
      type: 'textarea',
      access: {
        read: ({ req: { user } }) => user?.role === 'admin',
        create: ({ req: { user } }) => user?.role === 'admin',
        update: ({ req: { user } }) => user?.role === 'admin',
      },
    },
  ],
  
  // Document-level access
  access: {
    read: ({ req: { user } }) => {
      if (!user) {
        // Public can only read published posts
        return { status: { equals: 'published' } }
      }
      
      if (user.role === 'admin') {
        return true // Admin can read everything
      }
      
      // Users can read published posts or their own drafts
      return {
        or: [
          { status: { equals: 'published' } },
          {
            and: [
              { author: { equals: user.id } },
              { status: { equals: 'draft' } },
            ],
          },
        ],
      }
    },
    
    create: ({ req: { user } }) => {
      return user?.role === 'admin' || user?.role === 'editor'
    },
    
    update: ({ req: { user }, id }) => {
      if (user?.role === 'admin') return true
      
      // Users can only update their own posts
      return {
        author: { equals: user?.id },
      }
    },
    
    delete: ({ req: { user } }) => {
      return user?.role === 'admin'
    },
  },
}
```

### Dynamic Access Control

```typescript
const DynamicAccessCollection: CollectionConfig = {
  slug: 'projects',
  
  access: {
    read: async ({ req: { user } }) => {
      if (!user) return false
      
      if (user.role === 'admin') return true
      
      // Get user's team memberships
      const memberships = await req.payload.find({
        collection: 'team-memberships',
        where: {
          user: { equals: user.id },
        },
      })
      
      const teamIds = memberships.docs.map(membership => membership.team)
      
      // User can read projects from their teams
      return {
        team: { in: teamIds },
      }
    },
    
    create: async ({ req: { user }, data }) => {
      if (!user) return false
      
      // Check if user has permission to create projects in this team
      const teamMembership = await req.payload.findOne({
        collection: 'team-memberships',
        where: {
          and: [
            { user: { equals: user.id } },
            { team: { equals: data.team } },
            { role: { in: ['admin', 'manager'] } },
          ],
        },
      })
      
      return Boolean(teamMembership)
    },
  },
}
```

## Versioning and Drafts

### Configuration

```typescript
const VersionedCollection: CollectionConfig = {
  slug: 'articles',
  
  versions: {
    maxPerDoc: 50, // Keep maximum 50 versions per document
    
    drafts: {
      autosave: {
        interval: 2000, // Auto-save every 2 seconds
      },
      validate: false, // Don't validate drafts
    },
  },
  
  hooks: {
    afterChange: [
      async ({ doc, operation, req }) => {
        // Notify reviewers when article is ready for review
        if (doc.status === 'ready-for-review' && operation === 'update') {
          const reviewers = await req.payload.find({
            collection: 'users',
            where: { role: { equals: 'reviewer' } },
          })
          
          for (const reviewer of reviewers.docs) {
            await req.payload.sendEmail({
              to: reviewer.email,
              subject: `Article ready for review: ${doc.title}`,
              html: `Please review article: ${doc.title}`,
            })
          }
        }
      },
    ],
  },
  
  fields: [
    {
      name: 'title',
      type: 'text',
      required: true,
    },
    {
      name: 'content',
      type: 'richText',
    },
    {
      name: 'status',
      type: 'select',
      options: [
        { label: 'Draft', value: 'draft' },
        { label: 'Ready for Review', value: 'ready-for-review' },
        { label: 'Published', value: 'published' },
        { label: 'Archived', value: 'archived' },
      ],
      defaultValue: 'draft',
    },
  ],
}
```

### Working with Versions

```typescript
// Create a draft
const draftArticle = await payload.create({
  collection: 'articles',
  data: {
    title: 'My Draft Article',
    content: 'Draft content...',
    status: 'draft',
  },
  draft: true, // Save as draft
})

// Update draft without publishing
const updatedDraft = await payload.update({
  collection: 'articles',
  id: draftArticle.id,
  data: {
    content: 'Updated draft content...',
  },
  draft: true, // Keep as draft
})

// Publish the draft
const publishedArticle = await payload.update({
  collection: 'articles',
  id: draftArticle.id,
  data: {
    status: 'published',
  },
  draft: false, // Publish
})

// Find versions of a document
const versions = await payload.findVersions({
  collection: 'articles',
  where: {
    'parent.value': { equals: articleId },
  },
  sort: '-createdAt',
})

// Restore a specific version
const restoredVersion = await payload.restoreVersion({
  collection: 'articles',
  id: versionId,
})

// Compare versions
const currentDoc = await payload.findByID({
  collection: 'articles',
  id: articleId,
})

const previousVersion = await payload.findVersionByID({
  collection: 'articles',
  id: versionId,
})

// Custom version comparison
const differences = compareDocuments(currentDoc, previousVersion)
```

## File Upload Management

### Upload Collection Configuration

```typescript
const MediaCollection: CollectionConfig = {
  slug: 'media',
  
  upload: {
    // Static URL path for files
    staticURL: '/media',
    
    // Directory to store files
    staticDir: 'media',
    
    // Image resizing
    imageSizes: [
      {
        name: 'thumbnail',
        width: 300,
        height: 200,
        crop: 'center',
      },
      {
        name: 'card',
        width: 600,
        height: 400,
        crop: 'center',
      },
      {
        name: 'hero',
        width: 1200,
        height: 600,
        crop: 'center',
      },
    ],
    
    // File validation
    mimeTypes: ['image/*'],
    
    // Admin interface
    adminThumbnail: 'thumbnail',
    
    // File processing hooks
    hooks: {
      beforeChange: [
        ({ data, req }) => {
          // Auto-generate alt text if not provided
          if (!data.alt && data.filename) {
            data.alt = data.filename
              .replace(/\.[^/.]+$/, '') // Remove extension
              .replace(/[-_]/g, ' ') // Replace dashes/underscores with spaces
              .replace(/\b\w/g, l => l.toUpperCase()) // Capitalize words
          }
          
          return data
        },
      ],
      
      afterChange: [
        async ({ doc, req }) => {
          // Process image for SEO
          if (doc.mimeType?.startsWith('image/')) {
            await optimizeImageForSEO(doc, req)
          }
        },
      ],
    },
  },
  
  fields: [
    {
      name: 'alt',
      type: 'text',
      required: true,
    },
    {
      name: 'caption',
      type: 'richText',
    },
    {
      name: 'folder',
      type: 'relationship',
      relationTo: 'media-folders',
      admin: {
        position: 'sidebar',
      },
    },
  ],
  
  access: {
    read: () => true, // Public access
    create: ({ req: { user } }) => Boolean(user),
    update: ({ req: { user }, doc }) => {
      return user?.role === 'admin' || doc.uploadedBy === user?.id
    },
    delete: ({ req: { user } }) => user?.role === 'admin',
  },
}
```

### File Upload Operations

```typescript
// Upload single file
const uploadedFile = await payload.create({
  collection: 'media',
  data: {
    alt: 'Product image',
    caption: 'Main product photo',
  },
  filesToUpload: [
    {
      file: fileBuffer, // or file stream
      filename: 'product-image.jpg',
    },
  ],
})

// Upload multiple files
const uploadedFiles = await Promise.all(
  files.map(file => payload.create({
    collection: 'media',
    data: {
      alt: file.alt,
      folder: folderId,
    },
    filesToUpload: [
      {
        file: file.buffer,
        filename: file.name,
      },
    ],
  }))
)

// Update file metadata
const updatedFile = await payload.update({
  collection: 'media',
  id: fileId,
  data: {
    alt: 'Updated alt text',
    caption: 'Updated caption',
  },
})

// Replace file
const replacedFile = await payload.update({
  collection: 'media',
  id: fileId,
  data: {
    alt: 'New file alt text',
  },
  filesToUpload: [
    {
      file: newFileBuffer,
      filename: 'new-file.jpg',
    },
  ],
  overwriteExistingFiles: true,
})
```

## Database Queries and Optimization

### Complex Queries

```typescript
// Advanced where clauses
const complexQuery = await payload.find({
  collection: 'products',
  where: {
    and: [
      {
        or: [
          { title: { contains: 'laptop' } },
          { description: { contains: 'laptop' } },
          { 'category.name': { contains: 'computers' } },
        ],
      },
      {
        price: {
          greater_than_equal: 500,
          less_than_equal: 2000,
        },
      },
      {
        'variants.inventory': {
          greater_than: 0,
        },
      },
      {
        status: { equals: 'published' },
      },
      {
        not: {
          tags: { in: ['discontinued', 'clearance'] },
        },
      },
    ],
  },
  sort: ['-featured', 'price', '-createdAt'],
  limit: 20,
})

// Geospatial queries
const nearbyStores = await payload.find({
  collection: 'stores',
  where: {
    location: {
      near: [latitude, longitude, maxDistance],
    },
  },
})

// Date range queries
const recentOrders = await payload.find({
  collection: 'orders',
  where: {
    createdAt: {
      greater_than: new Date(Date.now() - 7 * 24 * 60 * 60 * 1000), // Last 7 days
      less_than: new Date(),
    },
  },
})

// Array field queries
const postsWithTags = await payload.find({
  collection: 'posts',
  where: {
    'tags.name': {
      in: ['javascript', 'typescript', 'react'],
    },
  },
})
```

### Performance Optimization

```typescript
// Use select to limit fields
const lightweightQuery = await payload.find({
  collection: 'products',
  select: {
    title: true,
    price: true,
    slug: true,
    // Exclude heavy fields like descriptions, images, etc.
  },
  limit: 100,
})

// Optimize relationships with depth
const productsWithCategories = await payload.find({
  collection: 'products',
  populate: {
    category: true, // Only populate direct category
    // Don't populate nested relationships
  },
  depth: 1, // Limit depth to avoid deep nesting
})

// Use indexes effectively
const indexedQuery = await payload.find({
  collection: 'products',
  where: {
    // This should use the compound index on [status, featured]
    status: { equals: 'published' },
    featured: { equals: true },
  },
  sort: 'createdAt', // Consider adding index on createdAt
})

// Batch operations for better performance
const batchUpdate = await payload.update({
  collection: 'products',
  where: {
    category: { equals: oldCategoryId },
  },
  data: {
    category: newCategoryId,
  },
})

// Use pagination for large datasets
const paginatedProducts = await payload.find({
  collection: 'products',
  limit: 50, // Keep reasonable page sizes
  page: pageNumber,
  pagination: true,
})
```

## TypeScript Integration

### Type-Safe Operations

```typescript
import type { DataFromCollectionSlug, RequiredDataFromCollectionSlug } from 'payload'

// Type-safe create data
type CreateProductData = RequiredDataFromCollectionSlug<'products'>

const createProduct = async (data: CreateProductData) => {
  const product = await payload.create({
    collection: 'products',
    data, // TypeScript ensures correct shape
  })
  
  return product // Correctly typed return
}

// Type-safe queries
type ProductQuery = {
  title?: string
  minPrice?: number
  maxPrice?: number
  categoryId?: string
}

const findProducts = async (query: ProductQuery) => {
  const where: any = {}
  
  if (query.title) {
    where.title = { contains: query.title }
  }
  
  if (query.minPrice || query.maxPrice) {
    where.price = {}
    if (query.minPrice) where.price.greater_than_equal = query.minPrice
    if (query.maxPrice) where.price.less_than_equal = query.maxPrice
  }
  
  if (query.categoryId) {
    where.category = { equals: query.categoryId }
  }
  
  return await payload.find({
    collection: 'products',
    where,
  })
}

// Custom operations with types
interface ProductService {
  createProduct(data: CreateProductData): Promise<DataFromCollectionSlug<'products'>>
  findProductsByCategory(categoryId: string): Promise<DataFromCollectionSlug<'products'>[]>
  updateProductPrice(id: string, price: number): Promise<DataFromCollectionSlug<'products'>>
}

class ProductServiceImpl implements ProductService {
  constructor(private payload: any) {}
  
  async createProduct(data: CreateProductData) {
    return await this.payload.create({
      collection: 'products',
      data,
    })
  }
  
  async findProductsByCategory(categoryId: string) {
    const result = await this.payload.find({
      collection: 'products',
      where: {
        category: { equals: categoryId },
      },
    })
    
    return result.docs
  }
  
  async updateProductPrice(id: string, price: number) {
    return await this.payload.update({
      collection: 'products',
      id,
      data: { price },
    })
  }
}
```

## Testing Collections

### Unit Tests

```typescript
import { jest } from '@jest/globals'
import { createOperation } from 'payload/collections/operations/create'

describe('Product Collection', () => {
  let mockReq: any
  let mockCollection: any
  
  beforeEach(() => {
    mockReq = {
      payload: {
        db: {
          create: jest.fn(),
        },
      },
      user: {
        id: 'user-123',
        role: 'admin',
      },
    }
    
    mockCollection = {
      config: {
        slug: 'products',
        fields: [],
        hooks: {},
        access: {
          create: () => true,
        },
      },
    }
  })
  
  it('should create a product successfully', async () => {
    const productData = {
      title: 'Test Product',
      price: 29.99,
      status: 'draft',
    }
    
    mockReq.payload.db.create.mockResolvedValue({
      id: 'product-123',
      ...productData,
    })
    
    const result = await createOperation({
      collection: mockCollection,
      data: productData,
      req: mockReq,
    })
    
    expect(result.title).toBe('Test Product')
    expect(result.price).toBe(29.99)
    expect(mockReq.payload.db.create).toHaveBeenCalledWith({
      collection: 'products',
      data: expect.objectContaining(productData),
      req: mockReq,
    })
  })
  
  it('should validate required fields', async () => {
    const invalidData = {
      price: 29.99,
      // Missing required title
    }
    
    await expect(
      createOperation({
        collection: mockCollection,
        data: invalidData,
        req: mockReq,
      })
    ).rejects.toThrow('Title is required')
  })
})
```

### Integration Tests

```typescript
import { getPayload } from 'payload'

describe('Product Collection Integration', () => {
  let payload: any
  
  beforeAll(async () => {
    payload = await getPayload({
      config: testConfig,
    })
  })
  
  afterAll(async () => {
    await payload.db.destroy()
  })
  
  beforeEach(async () => {
    // Clean database
    await payload.delete({
      collection: 'products',
      where: {},
    })
  })
  
  it('should handle complete product lifecycle', async () => {
    // Create product
    const product = await payload.create({
      collection: 'products',
      data: {
        title: 'Integration Test Product',
        price: 99.99,
        status: 'draft',
      },
    })
    
    expect(product.id).toBeDefined()
    expect(product.title).toBe('Integration Test Product')
    
    // Update product
    const updatedProduct = await payload.update({
      collection: 'products',
      id: product.id,
      data: {
        status: 'published',
      },
    })
    
    expect(updatedProduct.status).toBe('published')
    
    // Find product
    const foundProduct = await payload.findByID({
      collection: 'products',
      id: product.id,
    })
    
    expect(foundProduct.status).toBe('published')
    
    // Delete product
    await payload.delete({
      collection: 'products',
      id: product.id,
    })
    
    // Verify deletion
    await expect(
      payload.findByID({
        collection: 'products',
        id: product.id,
      })
    ).rejects.toThrow()
  })
})
```

## Troubleshooting

### Common Issues

#### "ValidationError: Field is required"
**Problem:** Required field validation failing

**Solution:**
```typescript
// Ensure all required fields are provided
const product = await payload.create({
  collection: 'products',
  data: {
    title: 'Product Title', // Required field
    price: 29.99, // Required field
    // ... other required fields
  },
})

// Check field configuration
const field = {
  name: 'title',
  type: 'text',
  required: true, // This field is required
  validate: (value) => {
    if (!value || value.trim() === '') {
      return 'Title cannot be empty'
    }
    return true
  },
}
```

#### "Access denied" Errors
**Problem:** Access control preventing operations

**Solution:**
```typescript
// Debug access control
const Collection: CollectionConfig = {
  access: {
    create: ({ req: { user } }) => {
      console.log('Create access check for user:', user)
      return user?.role === 'admin'
    },
  },
}

// Use overrideAccess for system operations
const systemProduct = await payload.create({
  collection: 'products',
  data: productData,
  overrideAccess: true, // Skip access control
})
```

#### Performance Issues
**Problem:** Slow queries and operations

**Solution:**
```typescript
// Add indexes for frequently queried fields
const Collection: CollectionConfig = {
  indexes: [
    {
      fields: ['status', 'featured'], // Compound index
    },
    {
      fields: ['createdAt'], // Single field index
    },
  ],
}

// Optimize queries
const optimizedQuery = await payload.find({
  collection: 'products',
  select: {
    title: true,
    price: true,
    // Only select needed fields
  },
  where: {
    status: { equals: 'published' }, // Use indexed field
  },
  limit: 20, // Limit results
  depth: 1, // Limit population depth
})
```

#### Hook Execution Order Issues
**Problem:** Hooks not executing in expected order

**Solution:**
```typescript
const Collection: CollectionConfig = {
  hooks: {
    // beforeValidate runs first
    beforeValidate: [
      ({ data }) => {
        console.log('1. Before validate')
        return data
      },
    ],
    
    // beforeChange runs after validation
    beforeChange: [
      ({ data }) => {
        console.log('2. Before change')
        return data
      },
    ],
    
    // afterChange runs after database operation
    afterChange: [
      ({ doc }) => {
        console.log('3. After change')
        return doc
      },
    ],
  },
}
```

## Migration Guide

### From v2 to v3

Key changes in collections system:

```typescript
// v2 (Old)
const collection = {
  slug: 'posts',
  fields: [
    {
      name: 'title',
      type: 'text',
      required: true,
    },
  ],
  hooks: {
    beforeChange: [
      ({ data, operation }) => {
        // Old hook signature
        return data
      },
    ],
  },
}

// v3 (New)
const collection: CollectionConfig = {
  slug: 'posts',
  fields: [
    {
      name: 'title',
      type: 'text',
      required: true,
    },
  ],
  hooks: {
    beforeChange: [
      ({ data, operation, originalDoc, req }) => {
        // New hook signature with more context
        return data
      },
    ],
  },
}

// Access control changes
// v2
access: {
  read: ({ req }) => {
    return req.user?.role === 'admin'
  }
}

// v3
access: {
  read: ({ req: { user } }) => {
    return user?.role === 'admin'
  }
}
```

## Performance Best Practices

### Query Optimization

```typescript
// Use specific selects
const lightQuery = await payload.find({
  collection: 'posts',
  select: {
    title: true,
    slug: true,
    publishedAt: true,
  },
})

// Limit depth for relationships
const shallowQuery = await payload.find({
  collection: 'posts',
  populate: {
    author: true, // Only populate author
  },
  depth: 1, // Don't go deeper
})

// Use efficient where clauses
const indexedQuery = await payload.find({
  collection: 'posts',
  where: {
    status: { equals: 'published' }, // Uses index
    featured: { equals: true }, // Uses compound index
  },
})
```

### Bulk Operations

```typescript
// Batch creates
const products = await payload.create({
  collection: 'products',
  data: [
    { title: 'Product 1', price: 10 },
    { title: 'Product 2', price: 20 },
    { title: 'Product 3', price: 30 },
  ],
})

// Bulk updates
await payload.update({
  collection: 'products',
  where: {
    category: { equals: 'electronics' },
  },
  data: {
    taxRate: 0.08,
  },
})
```

## Example Projects

- [E-commerce Collection Setup](https://github.com/payloadcms/payload/tree/main/examples/ecommerce) - Complete e-commerce collections
- [Blog with Comments](https://github.com/payloadcms/payload/tree/main/examples/blog) - Blog collections with relationships  
- [Multi-tenant Collections](https://github.com/payloadcms/payload/tree/main/examples/multi-tenant) - Tenant-scoped data access
- [Media Management](https://github.com/payloadcms/payload/tree/main/examples/custom-components) - Advanced file upload handling

## Contributing

Found a bug or have a suggestion? [Open an issue](https://github.com/payloadcms/payload/issues) or submit a Pull Request.

## License

MIT License - see the [LICENSE](https://github.com/payloadcms/payload/blob/main/LICENSE) file for details.