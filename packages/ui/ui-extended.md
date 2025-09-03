---
title: PayloadCMS UI Components
label: UI
order: 10
desc: Comprehensive React UI component library for PayloadCMS admin interface with forms, tables, drawers, and utilities.
keywords: [payloadcms, ui, components, react, forms, admin, hooks, providers, elements]
---

![NPM Version](https://img.shields.io/npm/v/@payloadcms/ui)
![Bundle Size](https://img.shields.io/bundlephobia/minzip/@payloadcms/ui)

## Overview

The `@payloadcms/ui` package is the comprehensive React component library that powers PayloadCMS's admin interface. It provides a complete set of UI components, form controls, data visualization elements, and utilities designed specifically for content management systems.

This package offers:
- Complete form system with field components for all PayloadCMS field types
- Data table and list view components with sorting, filtering, and pagination
- Modal and drawer system for overlaying content and actions
- Navigation, authentication, and layout components
- Hooks and providers for state management and context sharing
- Icon library and graphics optimized for admin interfaces

<Banner type="info">
The package is open-source. [View source code](https://github.com/payloadcms/payload/tree/main/packages/ui). Need help? [Community Help](https://payloadcms.com/community-help).
</Banner>

## System Requirements

- **PayloadCMS**: ^3.0.0 (workspace dependency)
- **Node.js**: ^18.20.2 || >=20.9.0
- **React**: ^19.0.0
- **React DOM**: ^19.0.0
- **Next.js**: ^15.2.3 (peer dependency)

## Installation

```bash
# npm
npm install @payloadcms/ui

# yarn
yarn add @payloadcms/ui

# pnpm
pnpm add @payloadcms/ui
```

### Peer Dependencies
This package requires the following peer dependencies:
```bash
npm install next@^15.2.3 payload@workspace:* react@^19.0.0 react-dom@^19.0.0
```

## Quick Start

Basic usage example showing form components and providers:

```typescript
'use client'
import { 
  Form, 
  TextField, 
  Button, 
  RootProvider,
  ConfigProvider 
} from '@payloadcms/ui'

// Basic form setup
export default function MyForm() {
  const handleSubmit = (formState) => {
    console.log('Form submitted:', formState)
  }

  return (
    <RootProvider>
      <ConfigProvider config={config}>
        <Form onSubmit={handleSubmit}>
          <TextField 
            name="title"
            label="Title"
            required
          />
          <Button type="submit">
            Save
          </Button>
        </Form>
      </ConfigProvider>
    </RootProvider>
  )
}
```

### Importing Styles
```typescript
// Import base styles
import '@payloadcms/ui/scss'

// Or import specific style files
import '@payloadcms/ui/scss/app.scss'
```

## Package Structure

### Export Paths

The package provides multiple export paths for different use cases:

- **Main Export** (`@payloadcms/ui`): Client-side components and hooks
- **Shared Export** (`@payloadcms/ui/shared`): Utilities that work on both client and server
- **RSC Export** (`@payloadcms/ui/rsc`): React Server Components
- **Individual Elements** (`@payloadcms/ui/elements/*`): Direct access to specific components
- **Icons** (`@payloadcms/ui/icons/*`): Individual icon components
- **Utilities** (`@payloadcms/ui/utilities/*`): Specific utility functions

```typescript
// Different import patterns
import { TextField, Button } from '@payloadcms/ui'
import { formatAdminURL } from '@payloadcms/ui/shared'
import { FieldDiffContainer } from '@payloadcms/ui/rsc'
import { CheckIcon } from '@payloadcms/ui/icons/Check'
import { buildFormState } from '@payloadcms/ui/utilities/buildFormState'
```

## Core Components

### Form Components

#### Form System
The form system provides comprehensive field management with validation, state tracking, and error handling:

```typescript
import { Form, useForm, useFormFields } from '@payloadcms/ui'

const MyForm = () => {
  const { 
    submit,
    formRef,
    processing,
    modified 
  } = useForm()
  
  const fields = useFormFields([
    { name: 'title', initialValue: '' },
    { name: 'description', initialValue: '' }
  ])

  return (
    <Form
      ref={formRef}
      onSubmit={submit}
      disabled={processing}
    >
      <TextField name="title" label="Title" />
      <TextareaField name="description" label="Description" />
      <Button type="submit" disabled={!modified}>
        {processing ? 'Saving...' : 'Save'}
      </Button>
    </Form>
  )
}
```

#### Field Components
Complete set of field components matching PayloadCMS field types:

```typescript
import {
  TextField,
  TextareaField,
  NumberField,
  CheckboxField,
  SelectField,
  DateTimeField,
  RelationshipField,
  UploadField,
  RichTextField,
  CodeField,
  JSONField,
  EmailField,
  PasswordField,
  RadioGroupField,
  ArrayField,
  BlocksField,
  GroupField,
  RowField,
  TabsField,
  CollapsibleField,
  UIField
} from '@payloadcms/ui'

// Text input with validation
<TextField 
  name="slug"
  label="URL Slug"
  required
  validate={(value) => {
    if (!/^[a-z0-9-]+$/.test(value)) {
      return 'Invalid slug format'
    }
  }}
/>

// Select with custom options
<SelectField
  name="status"
  label="Status"
  options={[
    { label: 'Draft', value: 'draft' },
    { label: 'Published', value: 'published' }
  ]}
/>

// Rich text editor
<RichTextField
  name="content"
  label="Content"
  admin={{
    upload: {
      collections: {
        media: {
          fields: []
        }
      }
    }
  }}
/>
```

### Data Display Components

#### Tables and Lists
Powerful data table components with sorting, filtering, and selection:

```typescript
import { 
  Table, 
  DefaultCell, 
  useListQuery,
  Pagination,
  PerPage 
} from '@payloadcms/ui'

const DataTable = () => {
  const {
    data,
    loading,
    page,
    sort,
    handlePageChange,
    handleSortChange
  } = useListQuery({
    collection: 'posts',
    limit: 25
  })

  const columns = [
    {
      accessor: 'title',
      Header: 'Title',
      Cell: ({ cell }) => <DefaultCell cell={cell} />
    },
    {
      accessor: 'status',
      Header: 'Status',
      Cell: ({ cell }) => (
        <Pill className={`status-${cell.value}`}>
          {cell.value}
        </Pill>
      )
    }
  ]

  return (
    <div>
      <Table
        data={data.docs}
        columns={columns}
        loading={loading}
        onSort={handleSortChange}
      />
      <Pagination
        page={page}
        totalPages={data.totalPages}
        onChange={handlePageChange}
      />
    </div>
  )
}
```

#### Modals and Drawers
Flexible overlay system for displaying content and forms:

```typescript
import { 
  Modal, 
  useModal,
  Drawer,
  DocumentDrawer,
  useDocumentDrawer 
} from '@payloadcms/ui'

// Basic modal
const MyModal = () => {
  const { openModal, closeModal, isModalOpen } = useModal()
  
  return (
    <>
      <Button onClick={() => openModal('my-modal')}>
        Open Modal
      </Button>
      
      <Modal
        slug="my-modal" 
        className="my-modal"
      >
        <h2>Modal Content</h2>
        <Button onClick={() => closeModal('my-modal')}>
          Close
        </Button>
      </Modal>
    </>
  )
}

// Document editing drawer
const EditDocument = ({ id, collectionSlug }) => {
  const [DocumentDrawerToggler, DocumentDrawer] = useDocumentDrawer({
    id,
    collectionSlug,
    onSave: (doc) => {
      console.log('Document saved:', doc)
    }
  })

  return (
    <>
      <DocumentDrawerToggler>
        Edit Document
      </DocumentDrawerToggler>
      <DocumentDrawer />
    </>
  )
}
```

### Navigation and Layout

#### Navigation Components
Built-in navigation components for admin interfaces:

```typescript
import { 
  AppHeader,
  NavGroup,
  useNav,
  Gutter
} from '@payloadcms/ui'

const AdminLayout = ({ children }) => {
  const { navOpen, setNavOpen } = useNav()

  return (
    <div className="admin-layout">
      <AppHeader />
      
      <nav className={`admin-nav ${navOpen ? 'open' : 'closed'}`}>
        <NavGroup
          label="Content"
          entities={[
            { slug: 'posts', label: 'Posts' },
            { slug: 'pages', label: 'Pages' }
          ]}
        />
      </nav>

      <main className="admin-content">
        <Gutter className="admin-gutter">
          {children}
        </Gutter>
      </main>
    </div>
  )
}
```

## Hooks

### Form Hooks
Comprehensive hooks for form state management:

```typescript
import {
  useField,
  useForm,
  useFormFields,
  useFormModified,
  useFormProcessing,
  useWatchForm
} from '@payloadcms/ui'

// Field-level state management  
const MyField = ({ name, label }) => {
  const {
    value,
    setValue,
    showError,
    errorMessage,
    validate
  } = useField({ path: name })

  return (
    <div className="field">
      <label>{label}</label>
      <input 
        value={value || ''}
        onChange={(e) => setValue(e.target.value)}
        onBlur={validate}
      />
      {showError && <span className="error">{errorMessage}</span>}
    </div>
  )
}

// Watch form state changes
const FormWatcher = () => {
  const formData = useWatchForm()
  
  useEffect(() => {
    console.log('Form data changed:', formData)
  }, [formData])

  return null
}
```

### Utility Hooks
General-purpose hooks for common UI patterns:

```typescript
import {
  useDebounce,
  useDebouncedCallback,
  useClickOutside,
  useHotkey,
  useIntersect,
  useResize,
  usePayloadAPI
} from '@payloadcms/ui'

// Debounced search
const SearchField = () => {
  const [query, setQuery] = useState('')
  const debouncedQuery = useDebounce(query, 300)
  
  const { data, loading } = usePayloadAPI({
    url: `/api/search?q=${debouncedQuery}`,
    skip: !debouncedQuery
  })

  return (
    <input
      placeholder="Search..."
      value={query}
      onChange={(e) => setQuery(e.target.value)}
    />
  )
}

// Click outside handler
const DropdownMenu = ({ children }) => {
  const [isOpen, setIsOpen] = useState(false)
  const menuRef = useRef()
  
  useClickOutside(menuRef, () => setIsOpen(false))
  
  return (
    <div ref={menuRef} className="dropdown">
      <button onClick={() => setIsOpen(!isOpen)}>
        Menu
      </button>
      {isOpen && (
        <div className="dropdown-content">
          {children}
        </div>
      )}
    </div>
  )
}

// Keyboard shortcuts
const ShortcutHandler = () => {
  useHotkey('cmd+s', (e) => {
    e.preventDefault()
    // Save action
  })

  useHotkey('esc', () => {
    // Close modal/drawer
  })

  return null
}
```

## Providers

### Core Providers
Essential context providers for PayloadCMS admin functionality:

```typescript
import {
  RootProvider,
  ConfigProvider,
  AuthProvider,
  LocaleProvider,
  ThemeProvider,
  TranslationProvider,
  RouteTransitionProvider
} from '@payloadcms/ui'

const App = ({ config, user, locale }) => {
  return (
    <RootProvider>
      <ConfigProvider config={config}>
        <AuthProvider user={user}>
          <LocaleProvider locale={locale}>
            <ThemeProvider theme="light">
              <TranslationProvider>
                <RouteTransitionProvider>
                  <AdminInterface />
                </RouteTransitionProvider>
              </TranslationProvider>
            </ThemeProvider>
          </LocaleProvider>
        </AuthProvider>
      </ConfigProvider>
    </RootProvider>
  )
}
```

### Specialized Providers
Context providers for specific functionality:

```typescript
import {
  SelectionProvider,
  useSelection,
  EditDepthProvider,
  useEditDepth,
  DocumentInfoProvider,
  useDocumentInfo,
  UploadHandlersProvider,
  useUploadHandlers
} from '@payloadcms/ui'

// Bulk selection management
const BulkActions = () => {
  const { 
    selected,
    selectAll,
    deselectAll,
    toggleSelection 
  } = useSelection()

  return (
    <div className="bulk-actions">
      <Button 
        onClick={selectAll}
        disabled={selected.length === totalDocs}
      >
        Select All ({selected.length})
      </Button>
      
      {selected.length > 0 && (
        <>
          <Button onClick={() => bulkDelete(selected)}>
            Delete Selected
          </Button>
          <Button onClick={() => bulkEdit(selected)}>
            Edit Selected
          </Button>
        </>
      )}
    </div>
  )
}
```

## Icons and Graphics

### Icon Components
Complete icon library optimized for admin interfaces:

```typescript
import {
  CheckIcon,
  ChevronIcon,
  EditIcon,
  DeleteIcon,
  PlusIcon,
  SearchIcon,
  MenuIcon,
  CloseMenuIcon,
  ExternalLinkIcon,
  CopyIcon,
  DragHandleIcon,
  FolderIcon,
  DocumentIcon,
  GridViewIcon,
  ListViewIcon
} from '@payloadcms/ui'

// Using icons in components
const ActionButton = ({ type, onClick, children }) => {
  const getIcon = () => {
    switch (type) {
      case 'edit': return <EditIcon />
      case 'delete': return <DeleteIcon />
      case 'add': return <PlusIcon />
      default: return null
    }
  }

  return (
    <Button onClick={onClick} className={`action-${type}`}>
      {getIcon()}
      {children}
    </Button>
  )
}
```

### Graphics Components
Branding and visual elements:

```typescript
import {
  PayloadIcon,
  PayloadLogo,
  Account,
  DefaultBlockImage,
  File
} from '@payloadcms/ui'

// Header with branding
const AdminHeader = () => {
  return (
    <header className="admin-header">
      <div className="brand">
        <PayloadLogo />
      </div>
      <div className="user-menu">
        <Account />
      </div>
    </header>
  )
}
```

## Utilities and Helpers

### Form State Management
Advanced utilities for managing complex form state:

```typescript
import {
  buildFormState,
  buildTableState,
  fieldSchemasToFormState,
  renderField
} from '@payloadcms/ui/utilities/buildFormState'

// Build form state from schema
const initializeForm = async (collectionSlug, docID) => {
  const formState = await buildFormState({
    id: docID,
    collectionSlug,
    operation: 'update',
    req: request,
    renderAllFields: true
  })

  return formState
}
```

### Client Configuration
Utilities for managing client-side configuration:

```typescript
import {
  getClientConfig,
  getClientSchemaMap,
  formatAdminURL
} from '@payloadcms/ui/shared'

// Get client-safe configuration
const clientConfig = getClientConfig({
  config: serverConfig,
  i18n: i18nInstance,
  importMap: payload.importMap
})

// Format admin URLs
const editURL = formatAdminURL({
  adminRoute: '/admin',
  route: `/collections/posts/edit/${docID}`
})
```

## Advanced Usage Patterns

### Custom Field Components
Creating custom field components that integrate with the form system:

```typescript
import { 
  useField,
  FieldLabel,
  FieldError,
  FieldDescription,
  fieldBaseClass
} from '@payloadcms/ui'

const CustomRatingField = ({ 
  name, 
  label, 
  description,
  required,
  admin 
}) => {
  const {
    value = 0,
    setValue,
    showError,
    errorMessage
  } = useField({ path: name })

  return (
    <div className={fieldBaseClass}>
      <FieldLabel 
        label={label}
        required={required}
      />
      
      <div className="rating-field">
        {[1, 2, 3, 4, 5].map(rating => (
          <button
            key={rating}
            type="button"
            className={`star ${value >= rating ? 'filled' : ''}`}
            onClick={() => setValue(rating)}
          >
            ★
          </button>
        ))}
      </div>
      
      <FieldDescription description={description} />
      <FieldError showError={showError} message={errorMessage} />
    </div>
  )
}

// Register custom field
export const customFieldComponents = {
  rating: CustomRatingField
}
```

### Custom List Views
Creating custom collection list views:

```typescript
import {
  DefaultListView,
  ListHeader,
  Table,
  useListQuery,
  ListSelection,
  GroupByHeader
} from '@payloadcms/ui'

const CustomPostsList = (props) => {
  const {
    collection,
    data,
    handleSortChange,
    hasCreatePermission,
    newDocumentURL
  } = props

  // Custom columns configuration
  const customColumns = [
    {
      accessor: 'title',
      Header: 'Title',
      Cell: ({ cell, row }) => (
        <Link href={`/admin/collections/posts/${row.id}`}>
          {cell.value}
        </Link>
      )
    },
    {
      accessor: 'status',
      Header: 'Status',
      Cell: ({ cell }) => (
        <Pill className={`status-${cell.value}`}>
          {cell.value}
        </Pill>
      )
    },
    {
      accessor: 'publishedAt',
      Header: 'Published',
      Cell: ({ cell }) => (
        cell.value ? new Date(cell.value).toLocaleDateString() : '-'
      )
    }
  ]

  return (
    <DefaultListView
      {...props}
      customColumns={customColumns}
      Header={(headerProps) => (
        <ListHeader {...headerProps}>
          <div className="custom-actions">
            <Button href="/admin/utilities/export-posts">
              Export Posts
            </Button>
          </div>
        </ListHeader>
      )}
    />
  )
}
```

## API Reference

### Core Components

#### Form Component
```typescript
interface FormProps {
  children: React.ReactNode
  onSubmit?: (formState: FormState) => void | Promise<void>
  method?: 'POST' | 'PATCH'
  action?: string
  disabled?: boolean
  className?: string
  id?: string
  onChange?: (formState: FormState) => void
  ref?: React.RefObject<HTMLFormElement>
}
```

#### Field Components
All field components share a common base interface:

```typescript
interface BaseFieldProps {
  name: string
  label?: string
  description?: string
  required?: boolean
  readOnly?: boolean
  admin?: {
    condition?: (data: any) => boolean
    className?: string
    style?: React.CSSProperties
    hidden?: boolean
  }
  validate?: (value: any) => string | true
}
```

#### Table Component
```typescript
interface TableProps {
  columns: Column[]
  data: any[]
  loading?: boolean
  onSort?: (column: string, direction: 'asc' | 'desc') => void
  appearance?: 'default' | 'minimal'
  className?: string
}
```

### Hook APIs

#### useField Hook
```typescript
interface UseFieldProps {
  path: string
  validate?: (value: any) => string | true
  condition?: (data: any) => boolean
}

interface UseFieldReturn {
  value: any
  setValue: (value: any) => void
  showError: boolean
  errorMessage?: string
  path: string
  validate: () => void
}
```

#### useForm Hook
```typescript
interface UseFormReturn {
  submit: (e?: React.FormEvent) => Promise<void>
  formRef: React.RefObject<HTMLFormElement>
  processing: boolean
  modified: boolean
  valid: boolean
  formState: FormState
  setFormState: (state: FormState) => void
}
```

## TypeScript Types

### Form State Types
```typescript
interface FormState {
  [key: string]: {
    value: any
    valid: boolean
    errorMessage?: string
    disableFormData?: boolean
  }
}

interface FieldAction {
  type: 'REPLACE_STATE' | 'UPDATE' | 'SET_PROCESSING' | 'SET_MODIFIED'
  payload?: any
}
```

### Component Types
```typescript
interface Column {
  accessor: string
  Header: string | React.ComponentType
  Cell?: React.ComponentType<{ cell: any, row: any }>
  sortable?: boolean
  width?: number
}

interface ListViewSlots {
  Header?: React.ComponentType
  Description?: React.ComponentType
  BeforeList?: React.ComponentType  
  AfterList?: React.ComponentType
}
```

## Styling and Theming

### SCSS Architecture
The package includes a comprehensive SCSS architecture:

```scss
// Import all styles
@import '@payloadcms/ui/scss';

// Or import specific components
@import '@payloadcms/ui/scss/app.scss';
```

### Theme Customization
```typescript
import { ThemeProvider, defaultTheme } from '@payloadcms/ui'

const customTheme = {
  ...defaultTheme,
  colors: {
    ...defaultTheme.colors,
    primary: '#your-brand-color',
    secondary: '#your-secondary-color'
  }
}

<ThemeProvider theme={customTheme}>
  {/* Your app */}
</ThemeProvider>
```

### CSS Custom Properties
The UI components use CSS custom properties that can be overridden:

```css
:root {
  --theme-elevation-0: #ffffff;
  --theme-elevation-50: #fafafa;
  --theme-elevation-100: #f5f5f5;
  --theme-elevation-200: #eeeeee;
  --theme-text: #333333;
  --theme-text-dim: #9a9a9a;
}
```

## Performance Considerations

### Code Splitting
The package is optimized for code splitting with multiple entry points:

```typescript
// Import only what you need
import { TextField } from '@payloadcms/ui/elements/TextField'
import { CheckIcon } from '@payloadcms/ui/icons/Check'

// Lazy load heavy components
const CodeEditor = lazy(() => import('@payloadcms/ui/elements/CodeEditor'))
```

### Bundle Analysis
The package includes optimizations for minimal bundle size:
- Tree-shakable exports
- Conditional loading of dependencies
- Lazy loading for heavy components (Monaco Editor, etc.)
- Optimized React compilation

## Troubleshooting

### Common Issues

#### "Cannot resolve module" errors
**Problem:** Import errors when using specific export paths

**Solution:**
```typescript
// Make sure you're using the correct import path
import { TextField } from '@payloadcms/ui' // ✅ Correct
import { TextField } from '@payloadcms/ui/fields/Text' // ❌ Incorrect

// For individual components, use elements path
import { TextField } from '@payloadcms/ui/elements/TextField' // ✅ Correct
```

#### Form state not updating
**Problem:** Form fields not reflecting state changes

**Solution:**
```typescript
// Ensure you're using the correct form context
const MyForm = () => {
  return (
    <Form> {/* Form provider is essential */}
      <TextField name="title" />
      {/* Components must be inside Form */}
    </Form>
  )
}

// For custom fields, ensure proper field registration
useField({ path: 'fieldName' }) // Must match the field name
```

#### Styling issues
**Problem:** Components not styled correctly

**Solution:**
```typescript
// Import required styles
import '@payloadcms/ui/scss'

// Ensure proper theme provider
<ThemeProvider theme={defaultTheme}>
  <YourComponents />
</ThemeProvider>
```

#### Server-side rendering issues
**Problem:** Components breaking during SSR

**Solution:**
```typescript
// Use client directive for client-only components
'use client'
import { SomeClientComponent } from '@payloadcms/ui'

// Use RSC exports for server components
import { ServerComponent } from '@payloadcms/ui/rsc'
```

### Debugging

#### Enable Debug Mode
```typescript
// Enable form debugging
<Form debug={true}>
  {/* Your fields */}
</Form>

// Check form state in DevTools
const formState = useWatchForm()
console.log('Current form state:', formState)
```

## Migration

### From Version 2.x to 3.x

**Breaking Changes:**
- React 19 requirement
- Next.js 15 requirement  
- Updated peer dependencies
- New export paths structure

**Migration Steps:**
```bash
# Update dependencies
npm install react@^19.0.0 react-dom@^19.0.0 next@^15.2.3

# Update imports
// Old (v2.x)
import { TextField } from '@payloadcms/ui/dist/fields/Text'

// New (v3.x)  
import { TextField } from '@payloadcms/ui'
```

## Example Projects

- [Custom Admin Interface](https://github.com/payloadcms/payload/tree/main/examples/custom-components) - Custom UI components
- [Form Builder](https://github.com/payloadcms/payload/tree/main/examples/form-builder) - Advanced form usage
- [Multi-tenant](https://github.com/payloadcms/payload/tree/main/examples/multi-tenant) - Complex admin interfaces

## Contributing

Found a bug or have a suggestion? [Open an issue](https://github.com/payloadcms/payload/issues) or submit a Pull Request.

## License

MIT License - Copyright (c) 2018-2025 Payload CMS, Inc.