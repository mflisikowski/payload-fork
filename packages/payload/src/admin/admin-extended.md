---
title: PayloadCMS Admin Interface System
label: Admin
order: 10
desc: Comprehensive admin panel framework with React components, form management, customizable views, and server-side rendering capabilities
keywords: [admin, ui, react, forms, components, customization, rsc, server-components, views, payload]
---

![NPM Version](https://img.shields.io/npm/v/payload)
![Bundle Size](https://img.shields.io/bundlephobia/minzip/payload)

## Overview

The PayloadCMS Admin Interface System is a comprehensive, highly customizable administrative interface built on React Server Components (RSCs). It provides a complete content management solution with sophisticated form handling, field components, view customization, and server-side rendering capabilities. This system enables developers to create powerful admin interfaces that integrate seamlessly with PayloadCMS's data layer and authentication system.

The admin system is designed for enterprise-grade applications, offering complete customization of forms, fields, views, and UI components while maintaining high performance through server-side rendering and intelligent client-side hydration. It supports complex workflows including document editing, list management, media handling, and custom administrative views.

<Banner type="info">
The package is open-source. [View source code](https://github.com/payloadcms/payload/tree/main/packages/payload/src/admin). Need help? [Community Help](https://payloadcms.com/community-help).
</Banner>

## System Requirements

- **PayloadCMS**: ^3.54.0
- **Node.js**: ^18.20.2 || >=20.9.0
- **React**: ^18.0.0 || ^19.0.0
- **Next.js**: ^15.0.0 (for RSC support)
- **TypeScript**: ^5.0.0 (recommended)

## Key Features

- 🎨 **Completely Customizable UI** - Override any component with custom React components
- 📝 **Advanced Form Management** - Sophisticated form state management with validation
- 🔧 **Server Components (RSC)** - Server-side rendering for better performance
- 📱 **Responsive Design** - Mobile-first responsive admin interface
- 🌍 **Internationalization** - Full i18n support with translation management
- 🎯 **Field Component System** - Rich set of field components for all data types
- 📊 **List & Table Views** - Powerful data browsing and management interfaces
- 🔍 **Advanced Filtering** - Complex filtering and search capabilities
- 📁 **Media Management** - Built-in file and media handling
- ⚡ **Performance Optimized** - Lazy loading and intelligent caching

## Architecture Overview

The admin system is built on several key architectural patterns:

### Component Architecture
- **Server Components**: Initial rendering happens on the server
- **Client Components**: Interactive elements hydrate on the client
- **Hybrid Rendering**: Optimal blend of server and client rendering

### Form System
- **Form State Management**: Centralized form state with validation
- **Field Components**: Modular field components for different data types
- **Server Validation**: Server-side validation with client-side feedback

### View System
- **Administrative Views**: Document, list, and custom views
- **Navigation**: Dynamic navigation based on collections and globals
- **Permissions**: Role-based access control throughout the interface

## Configuration

### Basic Admin Setup

```typescript
import { buildConfig } from 'payload'

export default buildConfig({
  admin: {
    // Basic admin configuration
    user: 'users', // Collection slug for admin users
    meta: {
      titleSuffix: '- My CMS',
      favicon: '/assets/favicon.ico',
      ogImage: '/assets/og-image.jpg',
    },
    
    // Custom CSS and styling
    css: '/assets/admin.css',
    
    // Disable admin panel (API-only mode)
    disable: false,
    
    // Custom build directory
    buildPath: '/admin',
    
    // Development options
    livePreview: {
      breakpoints: [
        { label: 'Mobile', name: 'mobile', width: 375, height: 667 },
        { label: 'Tablet', name: 'tablet', width: 768, height: 1024 },
        { label: 'Desktop', name: 'desktop', width: 1440, height: 900 },
      ],
    },
  },
  
  collections: [
    {
      slug: 'posts',
      admin: {
        // Collection-specific admin config
        useAsTitle: 'title',
        defaultColumns: ['title', 'status', 'createdAt'],
        group: 'Content',
        
        // Custom components
        components: {
          views: {
            list: {
              Component: '/components/CustomListView',
              actions: ['/components/CustomAction'],
            },
            edit: {
              Component: '/components/CustomEditView',
              tabs: [
                {
                  label: 'Content',
                  Component: '/components/ContentTab',
                },
                {
                  label: 'SEO',
                  Component: '/components/SEOTab',
                },
              ],
            },
          },
        },
      },
      fields: [
        {
          name: 'title',
          type: 'text',
          required: true,
          admin: {
            // Field-specific admin config
            position: 'sidebar',
            description: 'Enter the post title',
            placeholder: 'My awesome post...',
          },
        },
      ],
    },
  ],
})
```

### Advanced Customization

```typescript
import { buildConfig } from 'payload'

export default buildConfig({
  admin: {
    user: 'users',
    
    // Custom components
    components: {
      // Global admin components
      Nav: '/components/CustomNav',
      Logo: '/components/CustomLogo',
      
      // Account management
      account: '/components/CustomAccount',
      
      // Views
      views: {
        Dashboard: '/components/CustomDashboard',
        Account: '/components/CustomAccount',
      },
      
      // Graphics and branding
      graphics: {
        Logo: '/components/Logo',
        Icon: '/components/Icon',
      },
      
      // Actions
      actions: ['/components/GlobalAction'],
      
      // Head component for custom meta tags
      head: {
        Component: '/components/CustomHead',
      },
    },
    
    // Date formatting
    dateFormat: 'dd/MM/yyyy HH:mm:ss',
    
    // Auto-login for development
    autoLogin: {
      email: 'dev@payloadcms.com',
      password: 'test',
      prefillOnly: true,
    },
    
    // Theme configuration
    theme: 'dark',
  },
})
```

## Field Components

### Built-in Field Types

PayloadCMS provides a comprehensive set of field components:

```typescript
// Text-based fields
const textFields = {
  text: 'Single-line text input',
  textarea: 'Multi-line text input', 
  email: 'Email input with validation',
  code: 'Code editor with syntax highlighting',
  json: 'JSON editor with validation',
}

// Selection fields
const selectionFields = {
  select: 'Dropdown selection',
  radio: 'Radio button selection',
  checkbox: 'Single checkbox',
}

// Numeric fields
const numericFields = {
  number: 'Numeric input with validation',
  point: 'Geographic coordinates',
}

// Date and time
const dateFields = {
  date: 'Date/time picker',
}

// Relationships
const relationshipFields = {
  relationship: 'References to other documents',
  upload: 'File upload and media selection',
  join: 'Virtual relationships',
}

// Layout fields
const layoutFields = {
  group: 'Field grouping',
  array: 'Repeatable field groups',
  blocks: 'Dynamic content blocks',
  tabs: 'Tabbed field organization',
  row: 'Horizontal field arrangement',
  collapsible: 'Collapsible field sections',
  ui: 'Custom UI components',
}
```

### Custom Field Components

```typescript
// Custom field server component
export const CustomFieldServer: TextField['admin']['components']['Field'] = (props) => {
  const { 
    field,        // Field configuration
    value,        // Current field value
    setValue,     // Function to update value
    errorMessage, // Current error message
    readOnly,     // Read-only state
    req,          // PayloadRequest object
    user,         // Current user
    locale,       // Current locale
    i18n,         // Internationalization
  } = props
  
  // Server-side rendering logic
  return (
    <div className="custom-field">
      <label htmlFor={field.name}>
        {field.label}
        {field.required && <span className="required">*</span>}
      </label>
      
      <CustomInput 
        id={field.name}
        value={value}
        onChange={setValue}
        readOnly={readOnly}
        placeholder={field.admin?.placeholder}
      />
      
      {errorMessage && (
        <div className="field-error">{errorMessage}</div>
      )}
    </div>
  )
}

// Client component for interactivity
'use client'
export const CustomInput: React.FC<{
  id: string
  value: any
  onChange: (value: any) => void
  readOnly?: boolean
  placeholder?: string
}> = ({ id, value, onChange, readOnly, placeholder }) => {
  const [localValue, setLocalValue] = useState(value)
  
  const handleChange = useCallback((e: React.ChangeEvent<HTMLInputElement>) => {
    const newValue = e.target.value
    setLocalValue(newValue)
    onChange(newValue)
  }, [onChange])
  
  return (
    <input
      id={id}
      type="text"
      value={localValue || ''}
      onChange={handleChange}
      readOnly={readOnly}
      placeholder={placeholder}
      className="custom-input"
    />
  )
}

// Usage in field config
const customField: TextField = {
  name: 'customField',
  type: 'text',
  admin: {
    components: {
      Field: CustomFieldServer,
    },
  },
}
```

## Form State Management

### Form State Structure

```typescript
export interface FormState {
  [path: string]: FieldState
}

export interface FieldState {
  value?: unknown
  initialValue?: unknown
  valid?: boolean
  errorMessage?: string
  errorPaths?: string[]
  passesCondition?: boolean
  customComponents?: {
    Field?: React.ReactNode
    Label?: React.ReactNode
    Description?: React.ReactNode
    Error?: React.ReactNode
    BeforeInput?: React.ReactNode
    AfterInput?: React.ReactNode
  }
  filterOptions?: FilterOptionsResult
  validate?: Validate
  disableFormData?: boolean
  isModified?: boolean
  rows?: Row[]
}
```

### Working with Form State

```typescript
// Building form state
import { buildFormState } from 'payload'

const formState = await buildFormState({
  collectionSlug: 'posts',
  data: initialData,
  operation: 'create',
  req,
  docPermissions,
  docPreferences,
  schemaPath: 'posts',
  renderAllFields: true,
})

// Custom form component
'use client'
export const CustomForm: React.FC<{
  initialState: FormState
  onSubmit: (data: any) => void
}> = ({ initialState, onSubmit }) => {
  const [formState, setFormState] = useState(initialState)
  const [isSubmitting, setIsSubmitting] = useState(false)
  
  const updateField = useCallback((path: string, value: any) => {
    setFormState(prev => ({
      ...prev,
      [path]: {
        ...prev[path],
        value,
        isModified: true,
      }
    }))
  }, [])
  
  const handleSubmit = useCallback(async (e: React.FormEvent) => {
    e.preventDefault()
    setIsSubmitting(true)
    
    try {
      const data = extractFormData(formState)
      await onSubmit(data)
    } catch (error) {
      console.error('Form submission error:', error)
    } finally {
      setIsSubmitting(false)
    }
  }, [formState, onSubmit])
  
  return (
    <form onSubmit={handleSubmit}>
      {Object.entries(formState).map(([path, fieldState]) => (
        <FieldRenderer
          key={path}
          path={path}
          fieldState={fieldState}
          onUpdate={updateField}
        />
      ))}
      
      <button type="submit" disabled={isSubmitting}>
        {isSubmitting ? 'Saving...' : 'Save'}
      </button>
    </form>
  )
}

// Extracting form data
const extractFormData = (formState: FormState): Record<string, any> => {
  const data: Record<string, any> = {}
  
  Object.entries(formState).forEach(([path, fieldState]) => {
    if (!fieldState.disableFormData) {
      setNestedPath(data, path, fieldState.value)
    }
  })
  
  return data
}
```

## View Customization

### Custom List View

```typescript
// Custom list view server component
export const CustomListView: ListViewServerComponent = async ({
  collectionConfig,
  data,
  initPageResult,
  limit,
  req,
}) => {
  // Server-side data processing
  const processedData = await processListData(data, req)
  
  return (
    <div className="custom-list-view">
      <CustomListHeader collectionConfig={collectionConfig} />
      <CustomListFilters />
      <CustomListTable 
        data={processedData}
        columns={collectionConfig.admin.defaultColumns}
      />
      <CustomPagination 
        totalDocs={data.totalDocs}
        limit={limit}
        currentPage={data.page}
      />
    </div>
  )
}

// Custom document/edit view
export const CustomEditView: DocumentViewServerComponent = async ({
  collectionConfig,
  data,
  initPageResult,
  req,
}) => {
  const formState = await buildFormState({
    collectionSlug: collectionConfig.slug,
    data,
    operation: data?.id ? 'update' : 'create',
    req,
    docPermissions: initPageResult.permissions.collections?.[collectionConfig.slug],
    docPreferences: {},
    schemaPath: collectionConfig.slug,
    renderAllFields: true,
  })
  
  return (
    <div className="custom-edit-view">
      <CustomEditHeader 
        title={data?.[collectionConfig.admin.useAsTitle] || 'New Document'}
        status={data?.status}
      />
      
      <div className="edit-content">
        <CustomForm 
          formState={formState}
          collectionConfig={collectionConfig}
          initialData={data}
        />
        
        <CustomSidebar>
          <DocumentActions />
          <DocumentMetadata data={data} />
        </CustomSidebar>
      </div>
    </div>
  )
}
```

### Custom Dashboard

```typescript
// Custom dashboard component
export const CustomDashboard: AdminViewComponent = ({
  user,
  collectionConfigs,
  globalConfigs,
  permissions,
  req,
}) => {
  return (
    <div className="custom-dashboard">
      <DashboardHeader user={user} />
      
      <div className="dashboard-grid">
        <DashboardStats />
        <RecentActivity />
        <QuickActions 
          collections={collectionConfigs}
          permissions={permissions}
        />
        <SystemHealth />
      </div>
    </div>
  )
}

// Dashboard stats widget
const DashboardStats: React.FC = () => {
  const [stats, setStats] = useState(null)
  
  useEffect(() => {
    fetch('/api/admin/stats')
      .then(res => res.json())
      .then(setStats)
  }, [])
  
  return (
    <div className="dashboard-stats">
      <h2>Content Statistics</h2>
      {stats && (
        <div className="stats-grid">
          {Object.entries(stats).map(([collection, count]) => (
            <div key={collection} className="stat-item">
              <span className="stat-label">{collection}</span>
              <span className="stat-value">{count}</span>
            </div>
          ))}
        </div>
      )}
    </div>
  )
}
```

## Advanced Features

### Custom Navigation

```typescript
// Custom navigation component
export const CustomNav: React.FC<NavProps> = ({
  collections,
  globals,
  permissions,
  user,
}) => {
  const [collapsed, setCollapsed] = useState(false)
  
  return (
    <nav className={`admin-nav ${collapsed ? 'collapsed' : ''}`}>
      <div className="nav-header">
        <Logo />
        <button 
          className="nav-toggle"
          onClick={() => setCollapsed(!collapsed)}
        >
          {collapsed ? '→' : '←'}
        </button>
      </div>
      
      <div className="nav-sections">
        {/* Collections */}
        <NavSection title="Collections">
          {collections.map(collection => (
            <NavItem
              key={collection.slug}
              href={`/admin/collections/${collection.slug}`}
              icon={collection.admin?.icon}
              label={collection.admin?.group || collection.label}
              badge={collection.admin?.badge}
            />
          ))}
        </NavSection>
        
        {/* Globals */}
        <NavSection title="Globals">
          {globals.map(global => (
            <NavItem
              key={global.slug}
              href={`/admin/globals/${global.slug}`}
              icon={global.admin?.icon}
              label={global.label}
            />
          ))}
        </NavSection>
      </div>
      
      <div className="nav-footer">
        <UserMenu user={user} />
      </div>
    </nav>
  )
}
```

### Media Management

```typescript
// Custom upload field
export const CustomUploadField: UploadFieldServerComponent = ({
  field,
  value,
  setValue,
  collection,
}) => {
  const handleUpload = useCallback(async (files: FileList) => {
    const formData = new FormData()
    Array.from(files).forEach(file => {
      formData.append('file', file)
    })
    
    try {
      const response = await fetch(`/api/${collection.slug}`, {
        method: 'POST',
        body: formData,
      })
      
      if (response.ok) {
        const uploadedDoc = await response.json()
        setValue(uploadedDoc.doc)
      }
    } catch (error) {
      console.error('Upload error:', error)
    }
  }, [collection.slug, setValue])
  
  return (
    <div className="custom-upload-field">
      <div className="upload-area">
        {value ? (
          <MediaPreview media={value} onRemove={() => setValue(null)} />
        ) : (
          <DropZone onDrop={handleUpload} accept={field.filterOptions} />
        )}
      </div>
      
      <MediaBrowser
        collection={collection}
        onSelect={setValue}
        filterOptions={field.filterOptions}
      />
    </div>
  )
}

// Media browser component
const MediaBrowser: React.FC<{
  collection: any
  onSelect: (media: any) => void
  filterOptions?: any
}> = ({ collection, onSelect, filterOptions }) => {
  const [isOpen, setIsOpen] = useState(false)
  const [media, setMedia] = useState([])
  const [loading, setLoading] = useState(false)
  
  const loadMedia = useCallback(async () => {
    setLoading(true)
    try {
      const response = await fetch(`/api/${collection.slug}?limit=50`)
      const data = await response.json()
      setMedia(data.docs)
    } catch (error) {
      console.error('Failed to load media:', error)
    } finally {
      setLoading(false)
    }
  }, [collection.slug])
  
  useEffect(() => {
    if (isOpen) {
      loadMedia()
    }
  }, [isOpen, loadMedia])
  
  return (
    <>
      <button
        type="button"
        className="browse-media-btn"
        onClick={() => setIsOpen(true)}
      >
        Browse Media
      </button>
      
      {isOpen && (
        <Modal onClose={() => setIsOpen(false)}>
          <div className="media-browser">
            <div className="media-grid">
              {loading ? (
                <div>Loading...</div>
              ) : (
                media.map(item => (
                  <MediaItem
                    key={item.id}
                    media={item}
                    onClick={() => {
                      onSelect(item)
                      setIsOpen(false)
                    }}
                  />
                ))
              )}
            </div>
          </div>
        </Modal>
      )}
    </>
  )
}
```

## TypeScript Types

### Core Admin Types

```typescript
// Form state types
export interface FormState {
  [path: string]: FieldState
}

export interface FieldState {
  value?: unknown
  initialValue?: unknown
  valid?: boolean
  errorMessage?: string
  errorPaths?: string[]
  passesCondition?: boolean
  customComponents?: {
    Field?: React.ReactNode
    Label?: React.ReactNode
    Description?: React.ReactNode
    Error?: React.ReactNode
    BeforeInput?: React.ReactNode
    AfterInput?: React.ReactNode
  }
  filterOptions?: FilterOptionsResult
  validate?: Validate
  disableFormData?: boolean
  isModified?: boolean
  rows?: Row[]
  fieldSchema?: Field
  lastRenderedPath?: string
  selectFilterOptions?: Option[]
}

// View types
export type ViewTypes = 
  | 'account'
  | 'collection-folders' 
  | 'dashboard'
  | 'document'
  | 'folders'
  | 'list'
  | 'reset'
  | 'trash'
  | 'verify'
  | 'version'

export type AdminViewConfig = {
  Component: PayloadComponent
  exact?: boolean
  meta?: MetaConfig
  path?: `/${string}`
  sensitive?: boolean
  strict?: boolean
}

// Component types
export type AdminViewServerProps = {
  clientConfig: ClientConfig
  collectionConfig?: SanitizedCollectionConfig
  disableActions?: boolean
  docID?: number | string
  folderID?: number | string
  globalConfig?: SanitizedGlobalConfig
  importMap: ImportMap
  initialData?: Data
  initPageResult: InitPageResult
  params?: { [key: string]: string | string[] | undefined }
  redirectAfterCreate?: boolean
  redirectAfterDelete?: boolean
  redirectAfterDuplicate?: boolean
  redirectAfterRestore?: boolean
  viewType: ViewTypes
}

// Field component types
export type FieldServerComponent<
  TField extends Field = Field,
  TFieldClient extends ClientField = ClientField,
  TAdditionalProps = {}
> = React.ComponentType<ServerFieldBase<TField, TFieldClient> & TAdditionalProps>

export type FieldClientComponent<
  TFieldClient extends ClientField = ClientField,
  TAdditionalProps = {}
> = React.ComponentType<ClientFieldBase<TFieldClient> & TAdditionalProps>

// Server function types
export type ServerFunction<
  TArgs extends object = Record<string, unknown>,
  TReturnType = Promise<unknown> | unknown
> = (args: DefaultServerFunctionArgs & TArgs) => TReturnType

export type ServerFunctionConfig = {
  fn: ServerFunction
  name: string
}

// List and table types
export type ListQuery = {
  columns?: ColumnsFromURL
  groupBy?: string
  limit?: number
  page?: number
  preset?: number | string
  queryByGroup?: Record<string, ListQuery>
  search?: string
  sort?: Sort
  where?: Where
} & Record<string, unknown>

export type BuildTableStateArgs = {
  collectionSlug: string | string[]
  columns?: ColumnPreference[]
  data?: PaginatedDocs
  docs?: PaginatedDocs['docs']
  enableRowSelections?: boolean
  orderableFieldName: string
  parent?: {
    collectionSlug: CollectionSlug
    id: number | string
    joinPath: string
  }
  query?: ListQuery
  renderRowTypes?: boolean
  req: PayloadRequest
  tableAppearance?: 'condensed' | 'default'
}
```

## Usage Guides

### Creating Custom Field Components

```typescript
// 1. Define the field server component
import type { TextFieldServerComponent } from 'payload'

export const MyCustomFieldServer: TextFieldServerComponent = ({
  field,
  value,
  setValue,
  errorMessage,
  readOnly,
  req,
}) => {
  // Server-side logic and initial rendering
  return (
    <div className="custom-field-wrapper">
      <label htmlFor={field.name}>
        {field.label}
        {field.required && <span>*</span>}
      </label>
      
      {/* Client component for interactivity */}
      <MyCustomFieldClient
        initialValue={value}
        onChange={setValue}
        readOnly={readOnly}
        placeholder={field.admin?.placeholder}
      />
      
      {errorMessage && (
        <div className="error-message">{errorMessage}</div>
      )}
    </div>
  )
}

// 2. Create the interactive client component
'use client'
import { useCallback, useState } from 'react'

export const MyCustomFieldClient: React.FC<{
  initialValue: any
  onChange: (value: any) => void
  readOnly?: boolean
  placeholder?: string
}> = ({ initialValue, onChange, readOnly, placeholder }) => {
  const [value, setValue] = useState(initialValue)
  
  const handleChange = useCallback((e: React.ChangeEvent<HTMLInputElement>) => {
    const newValue = e.target.value
    setValue(newValue)
    onChange(newValue)
  }, [onChange])
  
  return (
    <input
      type="text"
      value={value || ''}
      onChange={handleChange}
      readOnly={readOnly}
      placeholder={placeholder}
      className="custom-input"
    />
  )
}

// 3. Use in field configuration
const customField: TextField = {
  name: 'myField',
  type: 'text',
  admin: {
    components: {
      Field: MyCustomFieldServer,
    },
  },
}
```

### Building Custom Views

```typescript
// Custom collection list view
import type { ListViewServerComponent } from 'payload'

export const CustomCollectionListView: ListViewServerComponent = async ({
  collectionConfig,
  data,
  initPageResult,
  limit,
  req,
}) => {
  // Server-side data processing
  const enhancedData = await enhanceListData(data, req)
  
  return (
    <div className="custom-list-view">
      <header className="list-header">
        <h1>{collectionConfig.labels.plural}</h1>
        <div className="list-actions">
          <CreateButton collectionSlug={collectionConfig.slug} />
          <ExportButton data={enhancedData} />
        </div>
      </header>
      
      <div className="list-controls">
        <SearchBox />
        <FilterControls fields={collectionConfig.fields} />
        <SortControls />
      </div>
      
      <CustomDataTable
        data={enhancedData}
        columns={collectionConfig.admin.defaultColumns}
        actions={['edit', 'delete', 'duplicate']}
      />
      
      <Pagination 
        totalDocs={data.totalDocs}
        limit={limit}
        page={data.page}
        totalPages={data.totalPages}
      />
    </div>
  )
}

// Register the custom view
const Posts: CollectionConfig = {
  slug: 'posts',
  admin: {
    components: {
      views: {
        list: {
          Component: CustomCollectionListView,
        },
      },
    },
  },
  fields: [/* ... */],
}
```

### Implementing Server Functions

```typescript
// Server function definition
import type { ServerFunction } from 'payload'

export const generateSitemap: ServerFunction<
  { domain: string },
  { sitemap: string; urls: number }
> = async ({ req, args }) => {
  const { domain } = args
  
  // Fetch all published posts
  const posts = await req.payload.find({
    collection: 'posts',
    where: {
      status: { equals: 'published' }
    },
    limit: 1000,
  })
  
  // Generate sitemap XML
  const urls = posts.docs.map(post => ({
    loc: `${domain}/posts/${post.slug}`,
    lastmod: post.updatedAt,
    changefreq: 'weekly',
    priority: '0.8',
  }))
  
  const sitemap = generateSitemapXML(urls)
  
  return {
    sitemap,
    urls: urls.length,
  }
}

// Client-side usage
'use client'
import { useServerFunction } from 'payload/client'

export const SitemapGenerator: React.FC = () => {
  const [sitemap, setSitemap] = useState<string>('')
  const [loading, setLoading] = useState(false)
  
  const generateSitemap = useServerFunction({
    name: 'generateSitemap',
  })
  
  const handleGenerate = useCallback(async () => {
    setLoading(true)
    try {
      const result = await generateSitemap({
        domain: 'https://mywebsite.com',
      })
      setSitemap(result.sitemap)
    } catch (error) {
      console.error('Failed to generate sitemap:', error)
    } finally {
      setLoading(false)
    }
  }, [generateSitemap])
  
  return (
    <div className="sitemap-generator">
      <button onClick={handleGenerate} disabled={loading}>
        {loading ? 'Generating...' : 'Generate Sitemap'}
      </button>
      
      {sitemap && (
        <textarea
          value={sitemap}
          readOnly
          rows={20}
          cols={80}
          className="sitemap-output"
        />
      )}
    </div>
  )
}
```

## Performance Optimization

### Server Component Best Practices

```typescript
// Optimize server components for performance
export const OptimizedListView: ListViewServerComponent = async ({
  data,
  req,
  collectionConfig,
}) => {
  // Pre-process data on server to minimize client work
  const processedData = useMemo(() => {
    return data.docs.map(doc => ({
      id: doc.id,
      title: doc.title,
      status: doc.status,
      createdAt: formatDate(doc.createdAt),
      // Only include necessary fields
    }))
  }, [data.docs])
  
  // Use React Server Components for static content
  return (
    <div className="optimized-list">
      {/* Server-rendered static header */}
      <ListHeader 
        title={collectionConfig.labels.plural}
        count={data.totalDocs}
      />
      
      {/* Client component only where interactivity is needed */}
      <InteractiveTable 
        initialData={processedData}
        totalPages={data.totalPages}
        currentPage={data.page}
      />
    </div>
  )
}

// Lazy load heavy components
const HeavyChartComponent = lazy(() => import('./HeavyChart'))

export const Dashboard: React.FC = () => {
  return (
    <div className="dashboard">
      <DashboardHeader />
      
      <Suspense fallback={<ChartSkeleton />}>
        <HeavyChartComponent />
      </Suspense>
    </div>
  )
}
```

### Form Performance

```typescript
// Optimize form rendering
'use client'
export const OptimizedForm: React.FC<{
  initialState: FormState
}> = ({ initialState }) => {
  const [formState, setFormState] = useState(initialState)
  const [changedFields, setChangedFields] = useState<Set<string>>(new Set())
  
  // Only re-render fields that have changed
  const updateField = useCallback((path: string, value: any) => {
    setFormState(prev => ({
      ...prev,
      [path]: {
        ...prev[path],
        value,
        isModified: true,
      }
    }))
    
    setChangedFields(prev => new Set(prev).add(path))
  }, [])
  
  // Memoize field components to prevent unnecessary re-renders
  const memoizedFields = useMemo(() => {
    return Object.entries(formState).map(([path, fieldState]) => (
      <MemoizedFieldRenderer
        key={path}
        path={path}
        fieldState={fieldState}
        onUpdate={updateField}
        hasChanged={changedFields.has(path)}
      />
    ))
  }, [formState, changedFields, updateField])
  
  return <form>{memoizedFields}</form>
}

// Memoized field renderer
const MemoizedFieldRenderer = React.memo<{
  path: string
  fieldState: FieldState
  onUpdate: (path: string, value: any) => void
  hasChanged: boolean
}>(({ path, fieldState, onUpdate, hasChanged }) => {
  return (
    <FieldRenderer
      path={path}
      fieldState={fieldState}
      onUpdate={onUpdate}
    />
  )
}, (prevProps, nextProps) => {
  // Only re-render if the field has actually changed
  return !nextProps.hasChanged && 
         prevProps.fieldState.value === nextProps.fieldState.value
})
```

## Internationalization

### Multi-language Admin Interface

```typescript
// Custom admin components with i18n
export const CustomButton: React.FC<{
  i18n: I18nClient
  onClick: () => void
}> = ({ i18n, onClick }) => {
  return (
    <button onClick={onClick} className="custom-button">
      {i18n.t('custom:button.save')}
    </button>
  )
}

// Language-aware field component
export const LocalizedFieldServer: TextFieldServerComponent = ({
  field,
  value,
  req,
  locale,
}) => {
  const { i18n } = req
  
  return (
    <div className="localized-field">
      <label>
        {i18n.t(`fields:${field.name}.label`)}
        <span className="locale-indicator">{locale}</span>
      </label>
      
      <LocalizedInput
        value={value}
        locale={locale}
        placeholder={i18n.t(`fields:${field.name}.placeholder`)}
      />
    </div>
  )
}

// Custom translation namespace
const translations = {
  en: {
    'custom:button.save': 'Save Changes',
    'custom:button.cancel': 'Cancel',
    'custom:message.success': 'Successfully saved!',
  },
  es: {
    'custom:button.save': 'Guardar Cambios',
    'custom:button.cancel': 'Cancelar', 
    'custom:message.success': '¡Guardado exitosamente!',
  },
}
```

## Troubleshooting

### Common Issues

#### "Component not found" Error
**Problem:** Custom components fail to load in admin interface

**Solution:**
1. Ensure component paths are correct in config
2. Check that components are properly exported
3. Verify RSC vs client component boundaries

```typescript
// Correct component export
export const MyCustomComponent: React.FC<Props> = (props) => {
  // Component implementation
}

// Correct config usage
components: {
  views: {
    list: {
      Component: '/path/to/MyCustomComponent', // Absolute path from project root
    },
  },
}
```

#### Form State Not Updating
**Problem:** Form fields don't reflect state changes

**Solution:**
```typescript
// Ensure proper state management
const MyFieldComponent = ({ value, onChange }) => {
  // Use controlled components
  return (
    <input
      value={value || ''}
      onChange={(e) => onChange(e.target.value)}
    />
  )
}

// Avoid uncontrolled components
const BadFieldComponent = ({ initialValue }) => {
  const [localValue, setLocalValue] = useState(initialValue)
  // This won't sync with form state!
  return <input value={localValue} onChange={...} />
}
```

#### Server Component Hydration Issues
**Problem:** Mismatch between server and client rendering

**Solution:**
```typescript
// Properly separate server and client logic
export const MyServerComponent = ({ data }) => {
  // Server-only logic
  return (
    <div>
      {/* Static server content */}
      <h1>{data.title}</h1>
      
      {/* Client component for interactivity */}
      <MyClientComponent initialData={data} />
    </div>
  )
}

'use client'
export const MyClientComponent = ({ initialData }) => {
  // Client-only interactivity
  const [state, setState] = useState(initialData)
  return <InteractiveElement />
}
```

### Debugging

#### Enable Admin Debug Mode

```typescript
export default buildConfig({
  admin: {
    // Enable detailed logging
    loggerOptions: {
      level: 'debug',
    },
    
    // Development helpers
    autoLogin: process.env.NODE_ENV === 'development' ? {
      email: 'admin@example.com',
      password: 'test',
    } : undefined,
  },
})
```

#### Component Debugging

```typescript
// Add debug logging to components
export const DebugComponent: React.FC<Props> = (props) => {
  useEffect(() => {
    console.log('Component props:', props)
  }, [props])
  
  return (
    <div data-debug="my-component">
      {/* Component content */}
    </div>
  )
}

// Form state debugging
export const useFormDebug = (formState: FormState) => {
  useEffect(() => {
    console.table(Object.entries(formState).map(([path, state]) => ({
      path,
      value: state.value,
      valid: state.valid,
      modified: state.isModified,
    })))
  }, [formState])
}
```

## Security Considerations

### Component Security

```typescript
// Sanitize user inputs in custom components
export const SafeHTMLField: React.FC<{
  value: string
  onChange: (value: string) => void
}> = ({ value, onChange }) => {
  const sanitizedValue = useMemo(() => {
    return DOMPurify.sanitize(value || '')
  }, [value])
  
  return (
    <div 
      dangerouslySetInnerHTML={{ __html: sanitizedValue }}
      onBlur={(e) => {
        const sanitized = DOMPurify.sanitize(e.currentTarget.innerHTML)
        onChange(sanitized)
      }}
    />
  )
}

// Validate permissions in custom views
export const SecureAdminView: AdminViewComponent = ({
  user,
  permissions,
  collectionConfig,
}) => {
  // Check permissions before rendering sensitive content
  if (!permissions.collections?.[collectionConfig.slug]?.read) {
    return <AccessDenied />
  }
  
  return <AdminContent />
}
```

## Migration Guide

### From v2 to v3

Key changes in the admin system:

```typescript
// v2 (Old approach)
const MyComponent = {
  path: '/components/MyComponent',
  serverProps: {
    someData: 'value'
  }
}

// v3 (New approach with RSCs)
export const MyComponent: AdminViewServerComponent = async ({
  req,
  initPageResult,
}) => {
  // Server logic runs here
  const data = await fetchServerData(req)
  
  return (
    <div>
      <ServerContent data={data} />
      <ClientInteractivity />
    </div>
  )
}
```

## Example Projects

- [Custom Admin Interface](https://github.com/payloadcms/payload/tree/main/examples/custom-components) - Complete admin customization
- [Advanced Forms](https://github.com/payloadcms/payload/tree/main/examples/form-builder) - Complex form implementations
- [Media Management](https://github.com/payloadcms/payload/tree/main/examples/custom-server) - Custom media handling
- [Multi-tenant Admin](https://github.com/payloadcms/payload/tree/main/examples/multi-tenant) - Multi-tenant interface patterns

## Contributing

Found a bug or have a suggestion? [Open an issue](https://github.com/payloadcms/payload/issues) or submit a Pull Request.

## License

MIT License - see the [LICENSE](https://github.com/payloadcms/payload/blob/main/LICENSE) file for details.