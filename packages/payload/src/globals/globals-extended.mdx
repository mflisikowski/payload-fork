---
title: PayloadCMS Globals System
label: Globals
order: 6
desc: Singleton data management system for site-wide settings, configuration, and shared content with versioning, access control, and live preview
keywords: [globals, singleton, settings, configuration, site-wide, shared-content, versioning, hooks, access-control]
---

![NPM Version](https://img.shields.io/npm/v/payload)
![Bundle Size](https://img.shields.io/bundlephobia/minzip/payload)

## Overview

The PayloadCMS Globals System provides a powerful singleton data management solution for site-wide settings, configuration values, and shared content that needs to exist as single instances rather than collections of documents. Globals are perfect for managing application settings, site configuration, navigation menus, footer content, SEO defaults, and any other data that should have only one instance per locale.

Unlike collections which manage multiple documents, globals handle single documents that can be accessed and updated throughout your application. The system includes comprehensive versioning support, advanced access control, hook integration, and live preview capabilities, making it ideal for managing critical site-wide data that requires careful change tracking and approval workflows.

The globals system integrates seamlessly with PayloadCMS's field system, supporting all field types including relationships, uploads, and complex nested structures, while providing the same level of type safety and validation as collections.

<Banner type="info">
The package is open-source. [View source code](https://github.com/payloadcms/payload/tree/main/packages/payload/src/globals). Need help? [Community Help](https://payloadcms.com/community-help).
</Banner>

## System Requirements

- **PayloadCMS**: ^3.54.0
- **Node.js**: ^18.20.2 || >=20.9.0
- **TypeScript**: ^5.0.0 (recommended)
- **Database**: MongoDB, PostgreSQL, SQLite, or other supported adapters

## Key Features

- 🔧 **Singleton Data Management** - Single instance data for site-wide settings
- 📝 **Comprehensive Field Support** - All field types including relationships and uploads
- 🎣 **Lifecycle Hooks** - Before/after hooks for validation and business logic
- 🔒 **Access Control** - Field-level and document-level permissions
- 📚 **Versioning & Drafts** - Track changes, draft management, and publishing
- 🌍 **Localization Support** - Multi-locale content management
- 👁️ **Live Preview** - Real-time preview of changes before publishing
- ⚡ **Performance Optimized** - Efficient caching and data retrieval
- 🎨 **Admin Customization** - Custom UI components and layouts
- 🔄 **API Generation** - Auto-generated REST and GraphQL endpoints

## Architecture Overview

The globals system follows a singleton pattern with these key components:

### Configuration Layer
- **Global Config**: Defines structure, fields, and behavior
- **Field Definitions**: Specifies data schema and validation rules
- **Access Patterns**: Configures permissions and security

### Operation Layer
- **Read/Update Operations**: Retrieve and modify singleton data
- **Versioning Operations**: Draft management and version control
- **Hook System**: Extensible lifecycle hooks

### Database Layer
- **Singleton Storage**: Optimized storage for single documents
- **Version Management**: Change tracking and history
- **Lock Management**: Concurrent editing protection

## Configuration

### Basic Global Setup

```typescript
import { GlobalConfig } from 'payload'

const SiteSettings: GlobalConfig = {
  slug: 'site-settings',
  
  // Global label for admin interface
  label: 'Site Settings',
  
  // Access control
  access: {
    read: () => true, // Everyone can read settings
    update: ({ req: { user } }) => {
      // Only admins can update settings
      return user?.role === 'admin'
    },
  },
  
  // Fields define the data structure
  fields: [
    {
      name: 'siteName',
      type: 'text',
      required: true,
      admin: {
        description: 'The name of your website',
      },
    },
    {
      name: 'logo',
      type: 'upload',
      relationTo: 'media',
      admin: {
        description: 'Site logo displayed in header',
      },
    },
    {
      name: 'tagline',
      type: 'text',
      admin: {
        description: 'Site tagline or slogan',
      },
    },
    {
      name: 'contact',
      type: 'group',
      fields: [
        {
          name: 'email',
          type: 'email',
          required: true,
        },
        {
          name: 'phone',
          type: 'text',
        },
        {
          name: 'address',
          type: 'textarea',
        },
      ],
    },
    {
      name: 'socialMedia',
      type: 'array',
      fields: [
        {
          name: 'platform',
          type: 'select',
          options: [
            { label: 'Facebook', value: 'facebook' },
            { label: 'Twitter', value: 'twitter' },
            { label: 'Instagram', value: 'instagram' },
            { label: 'LinkedIn', value: 'linkedin' },
          ],
          required: true,
        },
        {
          name: 'url',
          type: 'text',
          required: true,
          validate: (value) => {
            if (!value?.startsWith('http')) {
              return 'URL must start with http or https'
            }
            return true
          },
        },
      ],
    },
  ],
  
  // Admin interface configuration
  admin: {
    group: 'Settings',
    description: 'Manage global site settings and configuration',
  },
}
```

### Advanced Global Configuration

```typescript
import { GlobalConfig } from 'payload'

const NavigationGlobal: GlobalConfig = {
  slug: 'navigation',
  label: 'Navigation',
  
  // Access control with granular permissions
  access: {
    read: () => true,
    update: ({ req: { user } }) => {
      return ['admin', 'editor'].includes(user?.role)
    },
    readVersions: ({ req: { user } }) => {
      return user?.role === 'admin'
    },
  },
  
  // Lifecycle hooks for business logic
  hooks: {
    beforeChange: [
      ({ data, originalDoc }) => {
        // Auto-generate menu structure
        if (data.items) {
          data.items = data.items.map((item, index) => ({
            ...item,
            order: index,
            id: item.id || `item-${index}`,
          }))
        }
        
        return data
      },
    ],
    
    afterChange: [
      async ({ doc, req }) => {
        // Clear navigation cache after changes
        await req.payload.cache?.delete('navigation-cache')
        
        // Rebuild static pages that depend on navigation
        if (process.env.STATIC_REGENERATION_URL) {
          await fetch(`${process.env.STATIC_REGENERATION_URL}/api/revalidate`, {
            method: 'POST',
            headers: { 'Content-Type': 'application/json' },
            body: JSON.stringify({ path: '/navigation' }),
          })
        }
      },
    ],
  },
  
  fields: [
    {
      name: 'primaryNavigation',
      type: 'array',
      label: 'Primary Navigation',
      admin: {
        description: 'Main site navigation items',
      },
      fields: [
        {
          name: 'label',
          type: 'text',
          required: true,
        },
        {
          name: 'type',
          type: 'radio',
          options: [
            { label: 'Internal Link', value: 'internal' },
            { label: 'External Link', value: 'external' },
            { label: 'Page Reference', value: 'reference' },
          ],
          defaultValue: 'internal',
        },
        {
          name: 'url',
          type: 'text',
          admin: {
            condition: (data, siblingData) => siblingData.type === 'external',
          },
          validate: (value, { siblingData }) => {
            if (siblingData.type === 'external' && !value) {
              return 'URL is required for external links'
            }
            return true
          },
        },
        {
          name: 'internalUrl',
          type: 'text',
          admin: {
            condition: (data, siblingData) => siblingData.type === 'internal',
          },
        },
        {
          name: 'reference',
          type: 'relationship',
          relationTo: ['pages', 'posts'],
          admin: {
            condition: (data, siblingData) => siblingData.type === 'reference',
          },
        },
        {
          name: 'openInNewTab',
          type: 'checkbox',
          defaultValue: false,
        },
        {
          name: 'children',
          type: 'array',
          label: 'Dropdown Items',
          maxRows: 10,
          fields: [
            {
              name: 'label',
              type: 'text',
              required: true,
            },
            {
              name: 'url',
              type: 'text',
              required: true,
            },
            {
              name: 'icon',
              type: 'upload',
              relationTo: 'media',
            },
          ],
        },
      ],
      minRows: 1,
      maxRows: 8,
    },
    {
      name: 'footerNavigation',
      type: 'group',
      label: 'Footer Navigation',
      fields: [
        {
          name: 'columns',
          type: 'array',
          maxRows: 4,
          fields: [
            {
              name: 'title',
              type: 'text',
              required: true,
            },
            {
              name: 'links',
              type: 'array',
              fields: [
                {
                  name: 'label',
                  type: 'text',
                  required: true,
                },
                {
                  name: 'url',
                  type: 'text',
                  required: true,
                },
              ],
            },
          ],
        },
        {
          name: 'bottomLinks',
          type: 'array',
          label: 'Bottom Footer Links',
          fields: [
            {
              name: 'label',
              type: 'text',
              required: true,
            },
            {
              name: 'url',
              type: 'text',
              required: true,
            },
          ],
        },
      ],
    },
    {
      name: 'callToAction',
      type: 'group',
      label: 'Call to Action',
      fields: [
        {
          name: 'enabled',
          type: 'checkbox',
          defaultValue: false,
        },
        {
          name: 'text',
          type: 'text',
          admin: {
            condition: (data, siblingData) => siblingData.enabled,
          },
        },
        {
          name: 'url',
          type: 'text',
          admin: {
            condition: (data, siblingData) => siblingData.enabled,
          },
        },
      ],
    },
  ],
  
  // Enable versioning and drafts
  versions: {
    maxPerDoc: 25,
    drafts: {
      autosave: {
        interval: 3000, // Auto-save every 3 seconds
      },
    },
  },
  
  // Admin interface customization
  admin: {
    group: 'Content Management',
    description: 'Configure site navigation menus and links',
    
    // Custom components
    components: {
      views: {
        edit: {
          actions: ['/components/NavigationPreview'],
        },
      },
    },
    
    // Live preview
    livePreview: {
      url: ({ data }) => `${process.env.FRONTEND_URL}/preview/navigation`,
      breakpoints: [
        { label: 'Mobile', name: 'mobile', width: 375 },
        { label: 'Tablet', name: 'tablet', width: 768 },
        { label: 'Desktop', name: 'desktop', width: 1200 },
      ],
    },
  },
  
  // Custom API endpoints
  endpoints: [
    {
      path: '/menu/:type',
      method: 'get',
      handler: async (req, res) => {
        const { type } = req.params
        
        const navigation = await req.payload.findGlobal({
          slug: 'navigation',
          depth: 2,
        })
        
        if (type === 'primary') {
          res.json({ menu: navigation.primaryNavigation })
        } else if (type === 'footer') {
          res.json({ menu: navigation.footerNavigation })
        } else {
          res.status(400).json({ error: 'Invalid menu type' })
        }
      },
    },
  ],
}
```

## CRUD Operations

### Reading Global Data

```typescript
// Basic global retrieval
const siteSettings = await payload.findGlobal({
  slug: 'site-settings',
})

console.log(siteSettings.siteName) // Access global data

// Read with population and depth control
const navigationWithRefs = await payload.findGlobal({
  slug: 'navigation',
  depth: 2, // Populate relationships up to 2 levels deep
  populate: {
    'primaryNavigation.reference': true,
    'footerNavigation.columns.links': true,
  },
})

// Read with field selection
const lightweightSettings = await payload.findGlobal({
  slug: 'site-settings',
  select: {
    siteName: true,
    tagline: true,
    logo: true,
    // Exclude heavy fields
  },
})

// Read draft version
const draftNavigation = await payload.findGlobal({
  slug: 'navigation',
  draft: true, // Get draft version if available
})

// Server-side access with user context
const settingsForUser = await payload.findGlobal({
  slug: 'site-settings',
  user: req.user, // Apply access control based on user
  locale: 'es', // Get Spanish version
})

// Using local API (bypasses HTTP)
import { getPayload } from 'payload'

const payload = await getPayload({ config })
const settings = await payload.findGlobal({
  slug: 'site-settings',
  overrideAccess: true, // Skip access control for internal operations
})
```

### Updating Global Data

```typescript
// Basic global update
const updatedSettings = await payload.updateGlobal({
  slug: 'site-settings',
  data: {
    siteName: 'My Awesome Website',
    tagline: 'Building amazing experiences',
    contact: {
      email: 'hello@mywebsite.com',
      phone: '+1 (555) 123-4567',
    },
  },
})

// Update with file upload
const settingsWithLogo = await payload.updateGlobal({
  slug: 'site-settings',
  data: {
    logo: uploadedFileId, // Reference to uploaded media
    siteName: 'Updated Site Name',
  },
})

// Partial updates (merge with existing data)
const partialUpdate = await payload.updateGlobal({
  slug: 'site-settings',
  data: {
    'contact.email': 'newemail@example.com',
    'socialMedia.0.url': 'https://facebook.com/newpage',
  },
})

// Update as draft (versioning enabled)
const draftUpdate = await payload.updateGlobal({
  slug: 'navigation',
  data: navigationChanges,
  draft: true, // Save as draft without publishing
})

// Publish draft changes
const publishedNav = await payload.updateGlobal({
  slug: 'navigation',
  data: navigationChanges,
  draft: false, // Publish changes
})

// Localized updates
const localizedUpdate = await payload.updateGlobal({
  slug: 'site-settings',
  data: {
    siteName: 'Mi Sitio Web Increíble',
    tagline: 'Construyendo experiencias increíbles',
  },
  locale: 'es', // Update Spanish version
})

// Server-side update with hooks
const updateWithHooks = await payload.updateGlobal({
  slug: 'site-settings',
  data: settingsData,
  user: req.user,
  context: {
    triggerType: 'admin-update',
    source: 'dashboard',
  },
})
```

## Versioning and Drafts

### Version Management

```typescript
// Global with versioning enabled
const VersionedGlobal: GlobalConfig = {
  slug: 'content-settings',
  
  versions: {
    maxPerDoc: 50, // Keep up to 50 versions
    drafts: {
      autosave: {
        interval: 2000, // Auto-save every 2 seconds
      },
      validate: false, // Don't validate drafts
    },
  },
  
  fields: [
    {
      name: 'heroSection',
      type: 'group',
      fields: [
        { name: 'title', type: 'text', required: true },
        { name: 'subtitle', type: 'text' },
        { name: 'ctaText', type: 'text' },
      ],
    },
  ],
}

// Working with versions
const versions = await payload.findGlobalVersions({
  slug: 'content-settings',
  limit: 10,
  sort: '-createdAt',
})

console.log(`Found ${versions.totalDocs} versions`)

// Get specific version
const specificVersion = await payload.findGlobalVersionByID({
  slug: 'content-settings',
  id: versionId,
})

// Restore a version
const restoredGlobal = await payload.restoreGlobalVersion({
  slug: 'content-settings',
  id: versionId,
})

// Compare versions
const currentGlobal = await payload.findGlobal({
  slug: 'content-settings',
})

const previousVersion = await payload.findGlobalVersionByID({
  slug: 'content-settings',
  id: previousVersionId,
})

// Custom version comparison
const differences = compareGlobalVersions(currentGlobal, previousVersion)
```

### Draft Workflow

```typescript
// Create draft changes
const draftChanges = await payload.updateGlobal({
  slug: 'content-settings',
  data: {
    heroSection: {
      title: 'New Hero Title (Draft)',
      subtitle: 'This is a draft change',
    },
  },
  draft: true, // Save as draft
})

// Review draft in admin or via API
const draftContent = await payload.findGlobal({
  slug: 'content-settings',
  draft: true, // Get draft version
})

// Publish draft changes
const publishedContent = await payload.updateGlobal({
  slug: 'content-settings',
  data: draftContent,
  draft: false, // Publish the draft
})

// Auto-save functionality
const autoSaveGlobal: GlobalConfig = {
  slug: 'auto-save-demo',
  
  versions: {
    drafts: {
      autosave: {
        interval: 1000, // Auto-save every second
      },
    },
  },
  
  hooks: {
    beforeChange: [
      ({ data, req }) => {
        // Track auto-save events
        if (req.context?.autosave) {
          console.log('Auto-save triggered for global')
        }
        
        return data
      },
    ],
  },
  
  fields: [
    { name: 'content', type: 'richText' },
  ],
}
```

## Hook System

### Lifecycle Hooks

```typescript
const GlobalWithHooks: GlobalConfig = {
  slug: 'hooked-global',
  
  hooks: {
    // Before validation
    beforeValidate: [
      ({ data, originalDoc, req }) => {
        console.log('Before validate:', data)
        
        // Add timestamps
        if (!originalDoc) {
          data.createdAt = new Date().toISOString()
        }
        data.updatedAt = new Date().toISOString()
        
        return data
      },
    ],
    
    // Before change (after validation)
    beforeChange: [
      async ({ data, originalDoc, req }) => {
        // Sanitize data
        if (data.content) {
          data.content = sanitizeHtml(data.content)
        }
        
        // Validate business rules
        if (data.status === 'published' && !data.publishDate) {
          data.publishDate = new Date().toISOString()
        }
        
        // Create audit log
        await req.payload.create({
          collection: 'audit-logs',
          data: {
            action: 'global-update',
            globalSlug: 'hooked-global',
            userId: req.user?.id,
            changes: data,
            timestamp: new Date(),
          },
        })
        
        return data
      },
    ],
    
    // After change
    afterChange: [
      async ({ doc, previousDoc, req }) => {
        // Send notifications for important changes
        if (doc.status !== previousDoc?.status) {
          await sendStatusChangeNotification(doc, req)
        }
        
        // Clear related caches
        await clearGlobalCache('hooked-global')
        
        // Trigger webhooks
        await triggerWebhook('global.updated', {
          global: doc,
          previous: previousDoc,
        })
        
        // Update search index
        await updateSearchIndex('globals', doc)
      },
    ],
    
    // Before read
    beforeRead: [
      ({ doc, req }) => {
        // Track read access
        if (req.user) {
          trackGlobalAccess(doc, req.user)
        }
        
        return doc
      },
    ],
    
    // After read
    afterRead: [
      ({ doc, req }) => {
        // Add computed fields
        doc.isOwner = doc.createdBy === req.user?.id
        doc.canEdit = checkEditPermissions(doc, req.user)
        
        // Add metadata
        doc._metadata = {
          lastAccessed: new Date().toISOString(),
          accessedBy: req.user?.id,
        }
        
        return doc
      },
    ],
  },
  
  fields: [
    { name: 'title', type: 'text', required: true },
    { name: 'content', type: 'richText' },
    { name: 'status', type: 'select', options: ['draft', 'published'] },
    { name: 'publishDate', type: 'date' },
  ],
}

// Helper functions for hooks
const sanitizeHtml = (html: string) => {
  // Implement HTML sanitization
  return html.replace(/<script\b[^<]*(?:(?!<\/script>)<[^<]*)*<\/script>/gi, '')
}

const sendStatusChangeNotification = async (doc: any, req: any) => {
  if (doc.status === 'published') {
    await req.payload.sendEmail({
      to: 'admin@example.com',
      subject: `Global "${doc.title}" has been published`,
      html: `<p>The global content has been updated and published.</p>`,
    })
  }
}

const clearGlobalCache = async (slug: string) => {
  // Clear cache implementation
  console.log(`Clearing cache for global: ${slug}`)
}
```

## Access Control

### Basic Access Control

```typescript
const SecureGlobal: GlobalConfig = {
  slug: 'secure-settings',
  
  access: {
    // Read access
    read: ({ req: { user } }) => {
      // Everyone can read basic settings
      if (!user) return true
      
      // Admins can read everything
      if (user.role === 'admin') return true
      
      // Regular users can read non-sensitive fields
      return true
    },
    
    // Update access
    update: ({ req: { user } }) => {
      // Only admins and managers can update
      return ['admin', 'manager'].includes(user?.role)
    },
    
    // Version access
    readVersions: ({ req: { user } }) => {
      return user?.role === 'admin'
    },
  },
  
  fields: [
    {
      name: 'publicSettings',
      type: 'group',
      fields: [
        { name: 'siteName', type: 'text' },
        { name: 'description', type: 'textarea' },
      ],
      access: {
        read: () => true, // Public
        update: ({ req: { user } }) => user?.role === 'admin',
      },
    },
    {
      name: 'privateSettings',
      type: 'group',
      fields: [
        { name: 'apiKey', type: 'text' },
        { name: 'secretToken', type: 'text' },
      ],
      access: {
        read: ({ req: { user } }) => user?.role === 'admin',
        update: ({ req: { user } }) => user?.role === 'admin',
      },
    },
  ],
}
```

### Dynamic Access Control

```typescript
const DynamicAccessGlobal: GlobalConfig = {
  slug: 'tenant-settings',
  
  access: {
    read: async ({ req: { user } }) => {
      if (!user) return false
      
      // Super admin can access all tenant settings
      if (user.role === 'super-admin') return true
      
      // Users can only access their tenant's settings
      const userTenant = await req.payload.findOne({
        collection: 'tenants',
        where: {
          users: { contains: user.id },
        },
      })
      
      return userTenant ? { tenant: { equals: userTenant.id } } : false
    },
    
    update: async ({ req: { user } }) => {
      if (!user) return false
      
      // Check if user is tenant admin
      const tenantMembership = await req.payload.findOne({
        collection: 'tenant-memberships',
        where: {
          and: [
            { user: { equals: user.id } },
            { role: { equals: 'admin' } },
          ],
        },
      })
      
      return Boolean(tenantMembership)
    },
  },
  
  fields: [
    {
      name: 'tenant',
      type: 'relationship',
      relationTo: 'tenants',
      required: true,
      access: {
        update: () => false, // Prevent changing tenant assignment
      },
    },
    {
      name: 'settings',
      type: 'group',
      fields: [
        { name: 'theme', type: 'text' },
        { name: 'features', type: 'array', fields: [
          { name: 'name', type: 'text' },
          { name: 'enabled', type: 'checkbox' },
        ]},
      ],
    },
  ],
  
  hooks: {
    beforeChange: [
      async ({ data, req }) => {
        // Auto-assign tenant for new records
        if (!data.tenant && req.user?.tenant) {
          data.tenant = req.user.tenant
        }
        
        return data
      },
    ],
  },
}
```

## Admin Interface Customization

### Custom Components

```typescript
const CustomizedGlobal: GlobalConfig = {
  slug: 'customized-global',
  
  admin: {
    group: 'Advanced',
    description: 'Customized global with enhanced UI',
    
    components: {
      elements: {
        // Custom save button
        SaveButton: '/components/CustomSaveButton',
        
        // Custom publish button for drafts
        PublishButton: '/components/CustomPublishButton',
        
        // Custom description component
        Description: '/components/GlobalDescription',
        
        // Before document controls
        beforeDocumentControls: [
          '/components/StatusIndicator',
          '/components/LastModified',
        ],
      },
      
      views: {
        edit: {
          // Custom edit view
          Component: '/components/CustomGlobalEdit',
          
          // Custom actions
          actions: [
            '/components/ExportAction',
            '/components/ImportAction',
          ],
          
          // Tabs for organizing fields
          tabs: [
            {
              label: 'General',
              fields: ['title', 'description'],
            },
            {
              label: 'Advanced',
              fields: ['apiSettings', 'integrations'],
            },
            {
              label: 'SEO',
              fields: ['seoTitle', 'seoDescription'],
            },
          ],
        },
      },
    },
    
    // Live preview configuration
    livePreview: {
      url: ({ data }) => `${process.env.FRONTEND_URL}/preview/global`,
      breakpoints: [
        { label: 'Mobile', name: 'mobile', width: 375 },
        { label: 'Tablet', name: 'tablet', width: 768 },
        { label: 'Desktop', name: 'desktop', width: 1440 },
      ],
    },
  },
  
  fields: [
    {
      name: 'title',
      type: 'text',
      required: true,
      admin: {
        description: 'Main title for the global content',
      },
    },
    {
      name: 'content',
      type: 'richText',
      admin: {
        description: 'Rich text content with full formatting options',
      },
    },
    {
      name: 'apiSettings',
      type: 'group',
      admin: {
        description: 'API configuration and settings',
      },
      fields: [
        {
          name: 'enabled',
          type: 'checkbox',
          defaultValue: true,
        },
        {
          name: 'rateLimit',
          type: 'number',
          min: 1,
          max: 1000,
          defaultValue: 100,
        },
      ],
    },
  ],
}

// Custom component examples
// /components/CustomSaveButton.tsx
'use client'
import { SaveButtonClientProps, useFormSubmit } from 'payload'

export const CustomSaveButton: React.FC<SaveButtonClientProps> = ({
  disabled,
  label,
}) => {
  const { submit } = useFormSubmit()
  
  return (
    <button
      type="button"
      onClick={() => submit()}
      disabled={disabled}
      className="custom-save-button"
    >
      {label || 'Save Changes'} ✨
    </button>
  )
}

// /components/StatusIndicator.tsx
export const StatusIndicator: React.FC<{ data: any }> = ({ data }) => {
  const status = data?.status || 'draft'
  
  return (
    <div className={`status-indicator status-${status}`}>
      Status: {status.toUpperCase()}
      {data?.publishedAt && (
        <span className="published-date">
          Published: {new Date(data.publishedAt).toLocaleDateString()}
        </span>
      )}
    </div>
  )
}
```

## API Integration

### REST API Usage

```typescript
// Frontend API integration
class GlobalsAPI {
  private baseURL: string
  
  constructor(baseURL: string) {
    this.baseURL = baseURL
  }
  
  // Get global data
  async getGlobal(slug: string, options: {
    depth?: number
    locale?: string
    draft?: boolean
  } = {}) {
    const params = new URLSearchParams()
    
    if (options.depth) params.append('depth', options.depth.toString())
    if (options.locale) params.append('locale', options.locale)
    if (options.draft) params.append('draft', 'true')
    
    const response = await fetch(
      `${this.baseURL}/api/globals/${slug}?${params}`,
      {
        headers: {
          'Content-Type': 'application/json',
        },
      }
    )
    
    if (!response.ok) {
      throw new Error(`Failed to fetch global: ${response.statusText}`)
    }
    
    return response.json()
  }
  
  // Update global data
  async updateGlobal(slug: string, data: any, options: {
    locale?: string
    draft?: boolean
  } = {}) {
    const params = new URLSearchParams()
    
    if (options.locale) params.append('locale', options.locale)
    if (options.draft) params.append('draft', 'true')
    
    const response = await fetch(
      `${this.baseURL}/api/globals/${slug}?${params}`,
      {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
          'Authorization': `Bearer ${this.getAuthToken()}`,
        },
        body: JSON.stringify(data),
      }
    )
    
    if (!response.ok) {
      throw new Error(`Failed to update global: ${response.statusText}`)
    }
    
    return response.json()
  }
  
  // Get global versions
  async getGlobalVersions(slug: string, options: {
    limit?: number
    page?: number
    sort?: string
  } = {}) {
    const params = new URLSearchParams()
    
    if (options.limit) params.append('limit', options.limit.toString())
    if (options.page) params.append('page', options.page.toString())
    if (options.sort) params.append('sort', options.sort)
    
    const response = await fetch(
      `${this.baseURL}/api/globals/${slug}/versions?${params}`,
      {
        headers: {
          'Authorization': `Bearer ${this.getAuthToken()}`,
        },
      }
    )
    
    return response.json()
  }
  
  private getAuthToken(): string {
    // Get token from localStorage, cookie, etc.
    return localStorage.getItem('payload-token') || ''
  }
}

// Usage example
const globalsAPI = new GlobalsAPI('http://localhost:3000')

// Get site settings
const siteSettings = await globalsAPI.getGlobal('site-settings')

// Update navigation
await globalsAPI.updateGlobal('navigation', {
  primaryNavigation: [
    { label: 'Home', url: '/' },
    { label: 'About', url: '/about' },
    { label: 'Contact', url: '/contact' },
  ],
})

// Get versions
const versions = await globalsAPI.getGlobalVersions('navigation', {
  limit: 10,
  sort: '-createdAt',
})
```

### GraphQL Integration

```typescript
// GraphQL queries for globals
const GET_SITE_SETTINGS = `
  query GetSiteSettings($locale: LocaleInputType, $draft: Boolean) {
    SiteSettings(locale: $locale, draft: $draft) {
      siteName
      tagline
      logo {
        id
        url
        alt
        width
        height
      }
      contact {
        email
        phone
        address
      }
      socialMedia {
        platform
        url
      }
    }
  }
`

const UPDATE_SITE_SETTINGS = `
  mutation UpdateSiteSettings($data: mutationSiteSettingsInput!, $draft: Boolean) {
    updateSiteSettings(data: $data, draft: $draft) {
      siteName
      tagline
      updatedAt
    }
  }
`

// Usage with Apollo Client
import { useQuery, useMutation } from '@apollo/client'

export const useSiteSettings = (locale?: string, draft?: boolean) => {
  const { data, loading, error, refetch } = useQuery(GET_SITE_SETTINGS, {
    variables: { locale, draft },
    errorPolicy: 'all',
  })
  
  const [updateSettings] = useMutation(UPDATE_SITE_SETTINGS, {
    refetchQueries: [{ query: GET_SITE_SETTINGS, variables: { locale, draft } }],
  })
  
  return {
    siteSettings: data?.SiteSettings,
    loading,
    error,
    refetch,
    updateSettings: (newData: any, draftMode = false) =>
      updateSettings({
        variables: {
          data: newData,
          draft: draftMode,
        },
      }),
  }
}

// React component using the hook
export const SiteHeader: React.FC = () => {
  const { siteSettings, loading } = useSiteSettings()
  
  if (loading) return <div>Loading...</div>
  
  return (
    <header>
      <img src={siteSettings?.logo?.url} alt={siteSettings?.logo?.alt} />
      <h1>{siteSettings?.siteName}</h1>
      <p>{siteSettings?.tagline}</p>
    </header>
  )
}
```

## TypeScript Integration

### Type-Safe Operations

```typescript
import type { DataFromGlobalSlug } from 'payload'

// Type-safe global data access
type SiteSettingsData = DataFromGlobalSlug<'site-settings'>
type NavigationData = DataFromGlobalSlug<'navigation'>

// Type-safe global operations
class TypedGlobalsService {
  constructor(private payload: any) {}
  
  async getSiteSettings(): Promise<SiteSettingsData> {
    return await this.payload.findGlobal({
      slug: 'site-settings',
    })
  }
  
  async updateSiteSettings(
    data: Partial<SiteSettingsData>
  ): Promise<SiteSettingsData> {
    return await this.payload.updateGlobal({
      slug: 'site-settings',
      data,
    })
  }
  
  async getNavigation(options?: {
    locale?: string
    draft?: boolean
  }): Promise<NavigationData> {
    return await this.payload.findGlobal({
      slug: 'navigation',
      locale: options?.locale,
      draft: options?.draft,
    })
  }
  
  async updateNavigation(
    data: Partial<NavigationData>,
    draft = false
  ): Promise<NavigationData> {
    return await this.payload.updateGlobal({
      slug: 'navigation',
      data,
      draft,
    })
  }
}

// Usage with type safety
const globalsService = new TypedGlobalsService(payload)

const siteSettings = await globalsService.getSiteSettings()
// TypeScript knows the structure of siteSettings
console.log(siteSettings.siteName) // ✅ Type-safe access
console.log(siteSettings.invalidField) // ❌ TypeScript error

// Type-safe updates
await globalsService.updateSiteSettings({
  siteName: 'New Site Name',
  contact: {
    email: 'new@example.com',
    // phone and address are optional
  },
})
```

### Custom Global Types

```typescript
// Define custom interfaces for complex globals
interface NavigationItem {
  label: string
  type: 'internal' | 'external' | 'reference'
  url?: string
  internalUrl?: string
  reference?: {
    relationTo: 'pages' | 'posts'
    value: string
  }
  openInNewTab: boolean
  children?: NavigationItem[]
}

interface NavigationGlobal {
  primaryNavigation: NavigationItem[]
  footerNavigation: {
    columns: Array<{
      title: string
      links: Array<{
        label: string
        url: string
      }>
    }>
    bottomLinks: Array<{
      label: string
      url: string
    }>
  }
  callToAction: {
    enabled: boolean
    text?: string
    url?: string
  }
}

// Type-safe navigation utilities
class NavigationUtils {
  static buildMenuItems(items: NavigationItem[]): JSX.Element[] {
    return items.map((item, index) => {
      const href = this.getItemHref(item)
      
      return (
        <li key={index}>
          <a 
            href={href} 
            target={item.openInNewTab ? '_blank' : undefined}
            rel={item.openInNewTab ? 'noopener noreferrer' : undefined}
          >
            {item.label}
          </a>
          {item.children && item.children.length > 0 && (
            <ul className="dropdown">
              {this.buildMenuItems(item.children)}
            </ul>
          )}
        </li>
      )
    })
  }
  
  private static getItemHref(item: NavigationItem): string {
    switch (item.type) {
      case 'external':
        return item.url || '#'
      case 'internal':
        return item.internalUrl || '#'
      case 'reference':
        // Build URL from reference
        return item.reference ? `/${item.reference.relationTo}/${item.reference.value}` : '#'
      default:
        return '#'
    }
  }
}
```

## Performance Optimization

### Caching Strategies

```typescript
// Global with caching implementation
const CachedGlobal: GlobalConfig = {
  slug: 'cached-settings',
  
  hooks: {
    afterChange: [
      async ({ doc, req }) => {
        // Clear cache after changes
        await req.payload.cache?.delete(`global:${doc.globalType}`)
        await req.payload.cache?.delete(`global:${doc.globalType}:*`)
        
        // Warm up cache with new data
        await req.payload.cache?.set(
          `global:${doc.globalType}`,
          doc,
          3600 // Cache for 1 hour
        )
      },
    ],
    
    beforeRead: [
      async ({ req }) => {
        // Try to serve from cache
        const cached = await req.payload.cache?.get(`global:cached-settings`)
        if (cached) {
          req.context.servedFromCache = true
          return cached
        }
      },
    ],
  ],
  
  fields: [
    { name: 'title', type: 'text' },
    { name: 'content', type: 'richText' },
  ],
}

// Client-side caching with React Query
import { useQuery, useQueryClient } from '@tanstack/react-query'

export const useGlobalSettings = (slug: string, options?: {
  locale?: string
  draft?: boolean
}) => {
  const queryClient = useQueryClient()
  
  return useQuery({
    queryKey: ['global', slug, options],
    queryFn: async () => {
      const response = await fetch(`/api/globals/${slug}?${new URLSearchParams({
        ...(options?.locale && { locale: options.locale }),
        ...(options?.draft && { draft: 'true' }),
      })}`)
      
      if (!response.ok) {
        throw new Error('Failed to fetch global')
      }
      
      return response.json()
    },
    staleTime: 5 * 60 * 1000, // Consider data stale after 5 minutes
    cacheTime: 10 * 60 * 1000, // Keep in cache for 10 minutes
    refetchOnWindowFocus: false,
    onSuccess: (data) => {
      // Cache related data
      if (data.relatedGlobals) {
        data.relatedGlobals.forEach((global: any) => {
          queryClient.setQueryData(['global', global.slug], global)
        })
      }
    },
  })
}

// Cache invalidation helper
export const useGlobalMutation = () => {
  const queryClient = useQueryClient()
  
  return useMutation({
    mutationFn: async ({ slug, data }: { slug: string; data: any }) => {
      const response = await fetch(`/api/globals/${slug}`, {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify(data),
      })
      
      return response.json()
    },
    onSuccess: (data, variables) => {
      // Invalidate and update cache
      queryClient.invalidateQueries(['global', variables.slug])
      queryClient.setQueryData(['global', variables.slug], data)
      
      // Invalidate related queries
      queryClient.invalidateQueries(['global'])
    },
  })
}
```

### Database Optimization

```typescript
// Optimized global configuration
const OptimizedGlobal: GlobalConfig = {
  slug: 'optimized-global',
  
  // Select only necessary fields by default
  forceSelect: {
    id: true,
    globalType: true,
    updatedAt: true,
    // Force select critical fields for access control
  },
  
  fields: [
    {
      name: 'lightweightData',
      type: 'group',
      fields: [
        { name: 'title', type: 'text', index: true },
        { name: 'status', type: 'select', options: ['active', 'inactive'], index: true },
      ],
    },
    {
      name: 'heavyData',
      type: 'group',
      admin: {
        description: 'Large data that may not always be needed',
      },
      fields: [
        { name: 'largeContent', type: 'richText' },
        { name: 'mediaGallery', type: 'array', fields: [
          { name: 'image', type: 'upload', relationTo: 'media' },
        ]},
      ],
    },
  ],
  
  // Custom database name for optimization
  dbName: 'optimized_global_settings',
}

// Efficient data loading patterns
const loadGlobalEfficiently = async (slug: string, payload: any) => {
  // Load lightweight data first
  const basicData = await payload.findGlobal({
    slug,
    select: {
      'lightweightData.title': true,
      'lightweightData.status': true,
      globalType: true,
      updatedAt: true,
    },
    depth: 0, // Don't populate relationships initially
  })
  
  // Load heavy data only when needed
  if (basicData.lightweightData.status === 'active') {
    const fullData = await payload.findGlobal({
      slug,
      depth: 2, // Now we can afford to populate relationships
    })
    
    return fullData
  }
  
  return basicData
}
```

## Testing Globals

### Unit Tests

```typescript
import { jest } from '@jest/globals'

describe('Global Operations', () => {
  let mockPayload: any
  let mockReq: any
  
  beforeEach(() => {
    mockPayload = {
      findGlobal: jest.fn(),
      updateGlobal: jest.fn(),
    }
    
    mockReq = {
      user: { id: 'user-123', role: 'admin' },
      payload: mockPayload,
      context: {},
    }
  })
  
  it('should retrieve global data successfully', async () => {
    const mockGlobalData = {
      id: 'global-123',
      globalType: 'site-settings',
      siteName: 'Test Site',
      tagline: 'Test Tagline',
    }
    
    mockPayload.findGlobal.mockResolvedValue(mockGlobalData)
    
    const result = await mockPayload.findGlobal({
      slug: 'site-settings',
      user: mockReq.user,
    })
    
    expect(result.siteName).toBe('Test Site')
    expect(mockPayload.findGlobal).toHaveBeenCalledWith({
      slug: 'site-settings',
      user: mockReq.user,
    })
  })
  
  it('should update global data with validation', async () => {
    const updateData = {
      siteName: 'Updated Site Name',
      tagline: 'Updated Tagline',
    }
    
    const updatedGlobal = {
      ...updateData,
      id: 'global-123',
      globalType: 'site-settings',
      updatedAt: new Date().toISOString(),
    }
    
    mockPayload.updateGlobal.mockResolvedValue(updatedGlobal)
    
    const result = await mockPayload.updateGlobal({
      slug: 'site-settings',
      data: updateData,
      user: mockReq.user,
    })
    
    expect(result.siteName).toBe('Updated Site Name')
    expect(result.updatedAt).toBeDefined()
  })
  
  it('should handle access control correctly', async () => {
    const restrictedUser = { id: 'user-456', role: 'viewer' }
    
    mockPayload.findGlobal.mockRejectedValue(new Error('Access denied'))
    
    await expect(
      mockPayload.findGlobal({
        slug: 'admin-settings',
        user: restrictedUser,
      })
    ).rejects.toThrow('Access denied')
  })
})
```

### Integration Tests

```typescript
import { getPayload } from 'payload'

describe('Global Integration Tests', () => {
  let payload: any
  
  beforeAll(async () => {
    payload = await getPayload({
      config: testConfig,
    })
  })
  
  afterAll(async () => {
    await payload.db.destroy()
  })
  
  it('should handle complete global lifecycle', async () => {
    // Create initial global data
    const initialData = {
      siteName: 'Integration Test Site',
      tagline: 'Testing global operations',
      contact: {
        email: 'test@example.com',
        phone: '+1234567890',
      },
    }
    
    // Update global (creates if doesn't exist)
    const created = await payload.updateGlobal({
      slug: 'site-settings',
      data: initialData,
    })
    
    expect(created.siteName).toBe(initialData.siteName)
    expect(created.contact.email).toBe(initialData.contact.email)
    
    // Read global
    const retrieved = await payload.findGlobal({
      slug: 'site-settings',
    })
    
    expect(retrieved.siteName).toBe(initialData.siteName)
    
    // Update global
    const updateData = {
      siteName: 'Updated Site Name',
      tagline: 'Updated tagline',
    }
    
    const updated = await payload.updateGlobal({
      slug: 'site-settings',
      data: updateData,
    })
    
    expect(updated.siteName).toBe('Updated Site Name')
    expect(updated.contact.email).toBe(initialData.contact.email) // Should preserve existing data
    
    // Test versioning if enabled
    if (payload.config.globals.find((g: any) => g.slug === 'site-settings')?.versions) {
      const versions = await payload.findGlobalVersions({
        slug: 'site-settings',
      })
      
      expect(versions.totalDocs).toBeGreaterThan(0)
    }
  })
  
  it('should handle localization correctly', async () => {
    const englishData = {
      siteName: 'English Site Name',
      tagline: 'English tagline',
    }
    
    const spanishData = {
      siteName: 'Nombre del Sitio en Español',
      tagline: 'Lema en español',
    }
    
    // Update English version
    await payload.updateGlobal({
      slug: 'site-settings',
      data: englishData,
      locale: 'en',
    })
    
    // Update Spanish version
    await payload.updateGlobal({
      slug: 'site-settings',
      data: spanishData,
      locale: 'es',
    })
    
    // Verify English version
    const englishGlobal = await payload.findGlobal({
      slug: 'site-settings',
      locale: 'en',
    })
    
    expect(englishGlobal.siteName).toBe(englishData.siteName)
    
    // Verify Spanish version
    const spanishGlobal = await payload.findGlobal({
      slug: 'site-settings',
      locale: 'es',
    })
    
    expect(spanishGlobal.siteName).toBe(spanishData.siteName)
  })
})
```

## Troubleshooting

### Common Issues

#### "Global not found" Error
**Problem:** Attempting to access non-existent global

**Solution:**
```typescript
// Always check if global exists
const global = await payload.findGlobal({
  slug: 'my-settings',
}).catch(() => null)

if (!global) {
  // Handle missing global - create with defaults or show error
  console.log('Global not found, creating with defaults')
  
  return await payload.updateGlobal({
    slug: 'my-settings',
    data: {
      // Default values
      siteName: 'Default Site Name',
      status: 'active',
    },
  })
}
```

#### Access Control Issues
**Problem:** Access denied errors when reading/updating globals

**Solution:**
```typescript
// Debug access control
const GlobalWithDebugAccess: GlobalConfig = {
  slug: 'debug-global',
  access: {
    read: ({ req: { user } }) => {
      console.log('Read access check for user:', user)
      const hasAccess = Boolean(user)
      console.log('Access granted:', hasAccess)
      return hasAccess
    },
    update: ({ req: { user } }) => {
      console.log('Update access check for user:', user)
      const hasAccess = user?.role === 'admin'
      console.log('Update access granted:', hasAccess)
      return hasAccess
    },
  },
}

// Use overrideAccess for system operations
const systemGlobal = await payload.findGlobal({
  slug: 'my-settings',
  overrideAccess: true, // Skip access control
})
```

#### Version/Draft Issues
**Problem:** Drafts not working as expected

**Solution:**
```typescript
// Ensure versioning is properly configured
const VersionedGlobal: GlobalConfig = {
  slug: 'versioned-global',
  
  versions: {
    maxPerDoc: 10,
    drafts: {
      autosave: {
        interval: 2000,
      },
      validate: false, // Don't validate drafts
    },
  },
  
  hooks: {
    beforeChange: [
      ({ data, req }) => {
        // Debug version/draft operations
        console.log('Draft mode:', req.context?.draft)
        console.log('Data being saved:', data)
        return data
      },
    ],
  },
}

// Explicitly specify draft mode
const draftUpdate = await payload.updateGlobal({
  slug: 'my-global',
  data: changeData,
  draft: true, // Explicitly save as draft
})

const published = await payload.updateGlobal({
  slug: 'my-global',
  data: changeData,
  draft: false, // Explicitly publish
})
```

#### Performance Issues
**Problem:** Slow global operations

**Solution:**
```typescript
// Optimize field selection
const optimizedRead = await payload.findGlobal({
  slug: 'heavy-global',
  select: {
    // Only select needed fields
    title: true,
    status: true,
    // Don't select heavy fields like richText, arrays, etc.
  },
  depth: 0, // Don't populate relationships unless needed
})

// Use caching for frequently accessed globals
const cachedGlobal = await payload.findGlobal({
  slug: 'site-settings',
}).then(result => {
  // Cache the result
  cache.set('site-settings', result, 300) // Cache for 5 minutes
  return result
})
```

## Migration Guide

### From v2 to v3

Key changes in globals system:

```typescript
// v2 (Old)
const global = {
  slug: 'settings',
  fields: [
    {
      name: 'title',
      type: 'text',
    },
  ],
  hooks: {
    beforeChange: [
      ({ data }) => {
        // Old hook signature
        return data
      },
    ],
  },
}

// v3 (New)
const global: GlobalConfig = {
  slug: 'settings',
  fields: [
    {
      name: 'title',
      type: 'text',
    },
  ],
  hooks: {
    beforeChange: [
      ({ data, originalDoc, req }) => {
        // New hook signature with more context
        return data
      },
    ],
  },
}

// Access control changes
// v2
access: {
  read: ({ req }) => req.user?.role === 'admin'
}

// v3
access: {
  read: ({ req: { user } }) => user?.role === 'admin'
}
```

## Example Projects

- [Site Settings Management](https://github.com/payloadcms/payload/tree/main/examples/website) - Complete site settings global
- [Navigation System](https://github.com/payloadcms/payload/tree/main/examples/custom-components) - Dynamic navigation global
- [Multi-tenant Configuration](https://github.com/payloadcms/payload/tree/main/examples/multi-tenant) - Tenant-specific globals
- [SEO Management](https://github.com/payloadcms/payload/tree/main/examples/form-builder) - SEO defaults and configuration

## Contributing

Found a bug or have a suggestion? [Open an issue](https://github.com/payloadcms/payload/issues) or submit a Pull Request.

## License

MIT License - see the [LICENSE](https://github.com/payloadcms/payload/blob/main/LICENSE) file for details.