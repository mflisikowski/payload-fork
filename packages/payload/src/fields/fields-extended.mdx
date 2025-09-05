---
title: PayloadCMS Fields System
label: Fields
order: 3
desc: Comprehensive field system with 21+ field types, validation, hooks, access control, localization, and dynamic UI generation for content management
keywords: [fields, validation, hooks, access-control, ui-generation, field-types, schema, forms, content-management, typescript]
---

![NPM Version](https://img.shields.io/npm/v/payload)
![Bundle Size](https://img.shields.io/bundlephobia/minzip/payload)

## Overview

The PayloadCMS Fields System is the core data schema and form generation engine that powers all content management functionality in PayloadCMS. It provides a comprehensive suite of 21+ field types with built-in validation, extensive customization options, and a sophisticated hook system that enables complex data processing workflows. The fields system serves as the foundation for dynamic UI generation, database schema creation, and API endpoint generation.

This system is designed to handle complex content management scenarios while maintaining excellent developer experience through comprehensive TypeScript support, intuitive configuration patterns, and extensive customization capabilities. It supports everything from simple text fields to complex relational data structures, rich content editing, and dynamic content blocks.

The fields architecture emphasizes type safety, performance, and flexibility, enabling developers to create sophisticated content models while providing editors with intuitive interfaces for content management. Every field supports localization, access control, conditional display logic, and custom validation rules.

<Banner type="info">
The package is open-source. [View source code](https://github.com/payloadcms/payload/tree/main/packages/payload/src/fields). Need help? [Community Help](https://payloadcms.com/community-help).
</Banner>

## System Requirements

- **PayloadCMS**: ^3.54.0
- **Node.js**: ^18.20.2 || >=20.9.0
- **React**: ^18.0.0 || ^19.0.0 (for custom field components)
- **TypeScript**: ^5.0.0 (recommended for type safety)

## Key Features

- 🏗️ **21+ Field Types** - Complete set of field types for any content structure
- ✅ **Built-in Validation** - Comprehensive validation with custom rules support
- 🎣 **Lifecycle Hooks** - Five-stage hook system for data processing
- 🔒 **Access Control** - Field-level permissions with dynamic rules
- 🌍 **Localization** - Multi-language content support
- 🎨 **Custom Components** - Replace any field UI with custom React components
- 🔄 **Conditional Logic** - Show/hide fields based on other field values
- 📱 **Responsive UI** - Mobile-first admin interface generation
- 🔗 **Relationships** - Complex relational data modeling
- ⚡ **Performance** - Optimized for large forms and complex data structures

## Field Types Overview

PayloadCMS provides a comprehensive collection of field types organized into logical categories:

### Core Data Fields

#### Text Field
Single-line text input with comprehensive validation and array support.

```typescript
{
  name: 'title',
  type: 'text',
  required: true,
  minLength: 5,
  maxLength: 100,
  hasMany: false, // or true for arrays
  localized: true,
  index: true,
  unique: true,
  admin: {
    placeholder: 'Enter title...',
    description: 'The main title for this content',
  },
  validate: (value) => {
    if (value.includes('spam')) {
      return 'Title cannot contain spam'
    }
    return true
  },
}
```

#### Textarea Field
Multi-line text input for longer content.

```typescript
{
  name: 'description',
  type: 'textarea',
  required: true,
  minLength: 10,
  maxLength: 500,
  admin: {
    rows: 4,
    placeholder: 'Describe your content...',
  },
}
```

#### Email Field
Email input with built-in validation and authentication integration.

```typescript
{
  name: 'email',
  type: 'email',
  required: true,
  unique: true,
  admin: {
    placeholder: 'user@example.com',
  },
  validate: async (value, { req }) => {
    // Custom domain validation
    const allowedDomains = ['company.com', 'partner.org']
    const domain = value.split('@')[1]
    
    if (!allowedDomains.includes(domain)) {
      return `Email must be from: ${allowedDomains.join(', ')}`
    }
    return true
  },
}
```

#### Number Field
Numeric input with validation and array support.

```typescript
{
  name: 'price',
  type: 'number',
  required: true,
  min: 0,
  max: 10000,
  hasMany: false,
  admin: {
    step: 0.01,
    placeholder: '0.00',
    description: 'Price in USD',
  },
}
```

### Selection Fields

#### Select Field
Single or multi-select dropdown with dynamic options.

```typescript
{
  name: 'category',
  type: 'select',
  required: true,
  hasMany: false, // Set to true for multi-select
  options: [
    { label: 'Electronics', value: 'electronics' },
    { label: 'Clothing', value: 'clothing' },
    { label: 'Books', value: 'books' },
  ],
  // Dynamic options
  options: async ({ req }) => {
    const categories = await req.payload.find({
      collection: 'categories',
      limit: 100,
    })
    
    return categories.docs.map(cat => ({
      label: cat.name,
      value: cat.id,
    }))
  },
  // Filter options based on other fields
  filterOptions: async ({ relationTo, data, req }) => {
    if (data.type === 'premium') {
      return {
        premium: { equals: true }
      }
    }
    return {}
  },
}
```

#### Radio Field
Single selection from visible options.

```typescript
{
  name: 'priority',
  type: 'radio',
  required: true,
  options: [
    { label: 'Low', value: 'low' },
    { label: 'Medium', value: 'medium' },
    { label: 'High', value: 'high' },
    { label: 'Critical', value: 'critical' },
  ],
  defaultValue: 'medium',
  admin: {
    layout: 'horizontal', // or 'vertical'
  },
}
```

#### Checkbox Field
Boolean values with required validation support.

```typescript
{
  name: 'featured',
  type: 'checkbox',
  required: false,
  defaultValue: false,
  admin: {
    description: 'Display this item prominently',
  },
}
```

### Rich Content Fields

#### Rich Text Field
Advanced rich text editor with configurable features.

```typescript
{
  name: 'content',
  type: 'richText',
  required: true,
  localized: true,
  admin: {
    upload: {
      collections: {
        media: {
          fields: [
            {
              name: 'alt',
              type: 'text',
              required: true,
            },
          ],
        },
      },
    },
  },
  // Lexical editor configuration
  editor: lexicalEditor({
    features: ({ rootFeatures }) => [
      ...rootFeatures,
      HeadingFeature({ enabledHeadingSizes: ['h1', 'h2', 'h3'] }),
      BoldFeature(),
      ItalicFeature(),
      UnderlineFeature(),
      LinkFeature({
        enabledCollections: ['pages'],
      }),
      UploadFeature({
        collections: {
          media: {
            fields: [
              {
                name: 'alt',
                type: 'text',
                required: true,
              },
            ],
          },
        },
      }),
      BlockquoteFeature(),
      UnorderedListFeature(),
      OrderedListFeature(),
    ],
  }),
}
```

#### Code Field
Code editor with syntax highlighting.

```typescript
{
  name: 'snippet',
  type: 'code',
  required: true,
  admin: {
    language: 'javascript', // Default language
    editorOptions: {
      minimap: { enabled: false },
      wordWrap: 'on',
      lineNumbers: 'on',
      theme: 'vs-dark',
    },
  },
}
```

#### JSON Field
JSON editor with schema validation.

```typescript
{
  name: 'metadata',
  type: 'json',
  jsonSchema: {
    type: 'object',
    properties: {
      title: { type: 'string' },
      description: { type: 'string' },
      tags: {
        type: 'array',
        items: { type: 'string' },
      },
    },
    required: ['title'],
    additionalProperties: false,
  },
  admin: {
    description: 'Custom metadata in JSON format',
  },
}
```

### Date and Location Fields

#### Date Field
Date/time picker with timezone support.

```typescript
{
  name: 'publishedAt',
  type: 'date',
  required: true,
  defaultValue: () => new Date(),
  admin: {
    date: {
      pickerAppearance: 'dayAndTime',
      displayFormat: 'MM/dd/yyyy h:mm a',
      timeIntervals: 15,
    },
    description: 'When this content should be published',
  },
  // Timezone support
  admin: {
    date: {
      overrides: {
        timeZone: 'America/New_York',
      },
    },
  },
}
```

#### Point Field
Geographic coordinates storage.

```typescript
{
  name: 'location',
  type: 'point',
  required: true,
  admin: {
    description: 'Geographic coordinates [longitude, latitude]',
  },
  validate: ([longitude, latitude]) => {
    if (longitude < -180 || longitude > 180) {
      return 'Longitude must be between -180 and 180'
    }
    if (latitude < -90 || latitude > 90) {
      return 'Latitude must be between -90 and 90'
    }
    return true
  },
}
```

### Relational Fields

#### Relationship Field
References to other collections with filtering.

```typescript
{
  name: 'author',
  type: 'relationship',
  relationTo: 'users',
  hasMany: false,
  required: true,
  admin: {
    description: 'The author of this content',
  },
  // Filter available options
  filterOptions: ({ data }) => {
    return {
      role: { in: ['author', 'editor'] }
    }
  },
}

// Polymorphic relationships
{
  name: 'relatedContent',
  type: 'relationship',
  relationTo: ['posts', 'pages', 'media'],
  hasMany: true,
  maxRows: 5,
  admin: {
    description: 'Related content items',
  },
}
```

#### Upload Field
File uploads with media management.

```typescript
{
  name: 'featuredImage',
  type: 'upload',
  relationTo: 'media',
  required: true,
  admin: {
    description: 'Main image for this content',
  },
  // Filter by file type
  filterOptions: {
    mimeType: { contains: 'image' }
  },
}
```

#### Join Field
Virtual reverse relationship field.

```typescript
// In a Users collection
{
  name: 'posts',
  type: 'join',
  collection: 'posts',
  on: 'author',
  admin: {
    description: 'Posts written by this author',
  },
}
```

### Structural Fields

#### Array Field
Repeatable field groups with sorting.

```typescript
{
  name: 'features',
  type: 'array',
  required: true,
  minRows: 1,
  maxRows: 10,
  admin: {
    description: 'Key features of this product',
    initCollapsed: false,
  },
  fields: [
    {
      name: 'title',
      type: 'text',
      required: true,
    },
    {
      name: 'description',
      type: 'textarea',
      required: true,
    },
    {
      name: 'icon',
      type: 'upload',
      relationTo: 'media',
    },
  ],
}
```

#### Blocks Field
Dynamic content blocks with different types.

```typescript
{
  name: 'layout',
  type: 'blocks',
  required: true,
  minRows: 1,
  blocks: [
    {
      slug: 'hero',
      interfaceName: 'HeroBlock',
      fields: [
        {
          name: 'title',
          type: 'text',
          required: true,
        },
        {
          name: 'subtitle',
          type: 'text',
        },
        {
          name: 'backgroundImage',
          type: 'upload',
          relationTo: 'media',
        },
      ],
    },
    {
      slug: 'textBlock',
      interfaceName: 'TextBlock',
      fields: [
        {
          name: 'content',
          type: 'richText',
          required: true,
        },
      ],
    },
    {
      slug: 'imageGallery',
      interfaceName: 'ImageGallery',
      fields: [
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
              name: 'caption',
              type: 'text',
            },
          ],
        },
      ],
    },
  ],
  admin: {
    description: 'Flexible page layout blocks',
  },
}
```

#### Group Field
Field grouping for organization.

```typescript
{
  name: 'seo',
  type: 'group',
  interfaceName: 'SEO',
  admin: {
    description: 'Search Engine Optimization settings',
  },
  fields: [
    {
      name: 'title',
      type: 'text',
      maxLength: 60,
      admin: {
        description: 'Title tag for search engines',
      },
    },
    {
      name: 'description',
      type: 'textarea',
      maxLength: 160,
      admin: {
        description: 'Meta description for search engines',
      },
    },
    {
      name: 'keywords',
      type: 'text',
      hasMany: true,
      admin: {
        description: 'Keywords for this content',
      },
    },
    {
      name: 'ogImage',
      type: 'upload',
      relationTo: 'media',
      admin: {
        description: 'Open Graph image for social sharing',
      },
    },
  ],
}
```

### Layout Fields

#### Tabs Field
Organize fields into tabs.

```typescript
{
  name: 'contentTabs',
  type: 'tabs',
  tabs: [
    {
      label: 'Content',
      fields: [
        {
          name: 'title',
          type: 'text',
          required: true,
        },
        {
          name: 'content',
          type: 'richText',
          required: true,
        },
      ],
    },
    {
      label: 'Media',
      fields: [
        {
          name: 'featuredImage',
          type: 'upload',
          relationTo: 'media',
        },
        {
          name: 'gallery',
          type: 'array',
          fields: [
            {
              name: 'image',
              type: 'upload',
              relationTo: 'media',
            },
          ],
        },
      ],
    },
    {
      label: 'SEO',
      fields: [
        {
          name: 'seoTitle',
          type: 'text',
        },
        {
          name: 'seoDescription',
          type: 'textarea',
        },
      ],
    },
  ],
}
```

#### Row Field
Horizontal field layout.

```typescript
{
  name: 'dimensions',
  type: 'row',
  fields: [
    {
      name: 'width',
      type: 'number',
      required: true,
      admin: {
        width: '50%',
      },
    },
    {
      name: 'height',
      type: 'number',
      required: true,
      admin: {
        width: '50%',
      },
    },
  ],
}
```

#### Collapsible Field
Collapsible field sections.

```typescript
{
  name: 'advancedSettings',
  type: 'collapsible',
  label: 'Advanced Settings',
  admin: {
    initCollapsed: true,
    description: 'Advanced configuration options',
  },
  fields: [
    {
      name: 'customCSS',
      type: 'code',
      admin: {
        language: 'css',
      },
    },
    {
      name: 'customJS',
      type: 'code',
      admin: {
        language: 'javascript',
      },
    },
  ],
}
```

### Special Fields

#### UI Field
Custom UI components without data storage.

```typescript
{
  name: 'customComponent',
  type: 'ui',
  admin: {
    components: {
      Field: '/components/CustomUIField',
    },
    description: 'Custom interface element',
  },
}
```

## Field Configuration Options

Every field in PayloadCMS supports a comprehensive set of configuration options:

### Common Field Properties

```typescript
interface FieldBase {
  // Basic properties
  name: string
  type: FieldType
  required?: boolean
  unique?: boolean
  index?: boolean
  hidden?: boolean
  localized?: boolean
  defaultValue?: DefaultValue
  
  // Validation
  validate?: Validate
  
  // Access control
  access?: {
    create?: FieldAccess
    read?: FieldAccess
    update?: FieldAccess
  }
  
  // Hooks
  hooks?: {
    beforeValidate?: FieldHook[]
    beforeChange?: FieldHook[]
    afterChange?: FieldHook[]
    afterRead?: FieldHook[]
    beforeDuplicate?: FieldHook[]
  }
  
  // Admin interface
  admin?: {
    position?: 'main' | 'sidebar'
    width?: string
    description?: Description
    condition?: Condition
    disabled?: boolean
    readOnly?: boolean
    hidden?: boolean
    className?: string
    style?: CSSProperties
    placeholder?: string
    autoComplete?: string
    components?: {
      Field?: FieldComponent
      Cell?: CellComponent
      Label?: LabelComponent
      Description?: DescriptionComponent
      Error?: ErrorComponent
    }
  }
  
  // Custom properties
  custom?: Record<string, any>
  
  // Database
  dbName?: string
}
```

### Conditional Display Logic

Fields can be shown or hidden based on other field values:

```typescript
{
  name: 'discountAmount',
  type: 'number',
  admin: {
    condition: (data, siblingData) => {
      return data.hasDiscount === true
    },
  },
}

// More complex conditions
{
  name: 'shippingDetails',
  type: 'group',
  admin: {
    condition: (data) => {
      return data.productType === 'physical' && data.requiresShipping
    },
  },
  fields: [
    {
      name: 'weight',
      type: 'number',
    },
    {
      name: 'dimensions',
      type: 'row',
      fields: [
        { name: 'length', type: 'number' },
        { name: 'width', type: 'number' },
        { name: 'height', type: 'number' },
      ],
    },
  ],
}
```

## Field Hooks System

PayloadCMS provides a comprehensive hook system that allows you to execute custom logic at various stages of the field lifecycle:

### Hook Types

```typescript
// Available field hooks
interface FieldHooks {
  beforeValidate?: FieldHook[]
  beforeChange?: FieldHook[]
  afterChange?: FieldHook[]
  afterRead?: FieldHook[]
  beforeDuplicate?: FieldHook[]
}

// Hook function signature
type FieldHook<TValue = any, TData = any> = (
  args: FieldHookArgs<TData, TValue>
) => Promise<TValue> | TValue
```

### Hook Examples

#### beforeValidate Hook
Execute logic before field validation:

```typescript
{
  name: 'slug',
  type: 'text',
  required: true,
  hooks: {
    beforeValidate: [
      ({ value, data }) => {
        // Auto-generate slug from title if not provided
        if (!value && data?.title) {
          return data.title
            .toLowerCase()
            .replace(/[^a-z0-9]+/g, '-')
            .replace(/^-+|-+$/g, '')
        }
        return value
      },
    ],
  },
}
```

#### beforeChange Hook
Execute logic before saving to database:

```typescript
{
  name: 'email',
  type: 'email',
  hooks: {
    beforeChange: [
      ({ value, req }) => {
        // Always store emails in lowercase
        return value?.toLowerCase()
      },
    ],
  },
}

{
  name: 'content',
  type: 'richText',
  hooks: {
    beforeChange: [
      async ({ value, req }) => {
        // Process images in rich text
        if (value) {
          return await processRichTextImages(value, req)
        }
        return value
      },
    ],
  },
}
```

#### afterChange Hook
Execute logic after saving to database:

```typescript
{
  name: 'status',
  type: 'select',
  options: ['draft', 'published', 'archived'],
  hooks: {
    afterChange: [
      async ({ value, previousValue, data, req }) => {
        // Send notification when status changes to published
        if (value === 'published' && previousValue !== 'published') {
          await req.payload.sendEmail({
            to: 'editor@company.com',
            subject: `Content Published: ${data.title}`,
            html: `<p>The content "${data.title}" has been published.</p>`,
          })
        }
      },
    ],
  },
}
```

#### afterRead Hook
Execute logic when reading from database:

```typescript
{
  name: 'views',
  type: 'number',
  defaultValue: 0,
  hooks: {
    afterRead: [
      ({ value, req, doc }) => {
        // Don't expose view count to non-admin users
        if (req.user?.role !== 'admin') {
          return undefined
        }
        return value
      },
    ],
  },
}

{
  name: 'content',
  type: 'richText',
  hooks: {
    afterRead: [
      ({ value, req }) => {
        // Add computed reading time
        if (value) {
          const wordCount = countWords(value)
          const readingTime = Math.ceil(wordCount / 200) // 200 words per minute
          
          return {
            ...value,
            readingTime,
            wordCount,
          }
        }
        return value
      },
    ],
  },
}
```

#### beforeDuplicate Hook
Execute logic before document duplication:

```typescript
{
  name: 'title',
  type: 'text',
  hooks: {
    beforeDuplicate: [
      ({ value }) => {
        // Append "Copy" to title when duplicating
        return `${value} (Copy)`
      },
    ],
  },
}

{
  name: 'slug',
  type: 'text',
  hooks: {
    beforeDuplicate: [
      async ({ value, req }) => {
        // Generate unique slug for duplicate
        let newSlug = `${value}-copy`
        let counter = 1
        
        // Check if slug exists and increment
        while (await slugExists(newSlug, req)) {
          newSlug = `${value}-copy-${counter}`
          counter++
        }
        
        return newSlug
      },
    ],
  },
}
```

## Access Control

PayloadCMS provides granular access control at the field level:

### Basic Field Access

```typescript
{
  name: 'salary',
  type: 'number',
  access: {
    create: ({ req: { user } }) => {
      return user?.role === 'hr' || user?.role === 'admin'
    },
    read: ({ req: { user }, doc }) => {
      // HR and admin can read all salaries
      if (['hr', 'admin'].includes(user?.role)) return true
      
      // Users can only read their own salary
      return doc?.employee?.id === user?.id
    },
    update: ({ req: { user } }) => {
      return user?.role === 'hr' || user?.role === 'admin'
    },
  },
}
```

### Dynamic Access Control

```typescript
{
  name: 'internalNotes',
  type: 'textarea',
  access: {
    read: async ({ req: { user }, doc }) => {
      if (user?.role === 'admin') return true
      
      // Check if user is assigned to this project
      const assignment = await req.payload.findOne({
        collection: 'project-assignments',
        where: {
          and: [
            { project: { equals: doc.id } },
            { user: { equals: user?.id } },
            { role: { in: ['manager', 'lead'] } },
          ],
        },
      })
      
      return Boolean(assignment)
    },
    update: ({ req: { user } }) => {
      return ['admin', 'manager'].includes(user?.role)
    },
  },
}
```

### Field-Level Filtering

```typescript
{
  name: 'assignedTo',
  type: 'relationship',
  relationTo: 'users',
  access: {
    read: ({ req: { user } }) => {
      // Only show users from the same department
      if (user?.role !== 'admin') {
        return {
          department: { equals: user?.department }
        }
      }
      return true
    },
  },
  filterOptions: ({ req: { user } }) => {
    // Filter available users based on department
    if (user?.role !== 'admin') {
      return {
        department: { equals: user?.department },
        active: { equals: true },
      }
    }
    return { active: { equals: true } }
  },
}
```

## Validation System

PayloadCMS provides built-in validation for all field types plus custom validation support:

### Built-in Validation

```typescript
// Text field validation
{
  name: 'username',
  type: 'text',
  required: true,
  minLength: 3,
  maxLength: 20,
  unique: true,
  validate: (value) => {
    const usernameRegex = /^[a-zA-Z0-9_-]+$/
    if (!usernameRegex.test(value)) {
      return 'Username can only contain letters, numbers, hyphens, and underscores'
    }
    return true
  },
}

// Number field validation
{
  name: 'age',
  type: 'number',
  required: true,
  min: 0,
  max: 120,
  validate: (value) => {
    if (value < 18) {
      return 'Must be 18 or older'
    }
    return true
  },
}

// Email field validation
{
  name: 'email',
  type: 'email',
  required: true,
  validate: async (value, { req }) => {
    // Check if email domain is allowed
    const domain = value.split('@')[1]
    const allowedDomains = await req.payload.findGlobal({
      slug: 'site-settings',
      select: { allowedEmailDomains: true },
    })
    
    if (!allowedDomains.allowedEmailDomains.includes(domain)) {
      return `Email domain ${domain} is not allowed`
    }
    return true
  },
}
```

### Custom Validation Functions

```typescript
// Complex validation with multiple conditions
{
  name: 'password',
  type: 'text',
  required: true,
  validate: (value) => {
    const errors = []
    
    if (value.length < 8) {
      errors.push('Password must be at least 8 characters')
    }
    
    if (!/[A-Z]/.test(value)) {
      errors.push('Password must contain an uppercase letter')
    }
    
    if (!/[a-z]/.test(value)) {
      errors.push('Password must contain a lowercase letter')
    }
    
    if (!/\d/.test(value)) {
      errors.push('Password must contain a number')
    }
    
    if (!/[!@#$%^&*(),.?":{}|<>]/.test(value)) {
      errors.push('Password must contain a special character')
    }
    
    return errors.length > 0 ? errors.join(', ') : true
  },
}

// Async validation
{
  name: 'apiKey',
  type: 'text',
  required: true,
  validate: async (value, { req }) => {
    try {
      const response = await fetch('https://api.service.com/validate', {
        method: 'POST',
        headers: { 'Authorization': `Bearer ${value}` },
      })
      
      if (!response.ok) {
        return 'Invalid API key'
      }
      
      return true
    } catch (error) {
      return 'Could not validate API key'
    }
  },
}

// Cross-field validation
{
  name: 'confirmPassword',
  type: 'text',
  required: true,
  validate: (value, { data }) => {
    if (value !== data.password) {
      return 'Passwords do not match'
    }
    return true
  },
}
```

### Array Field Validation

```typescript
{
  name: 'tags',
  type: 'text',
  hasMany: true,
  minRows: 1,
  maxRows: 10,
  validate: (values) => {
    if (values.length === 0) {
      return 'At least one tag is required'
    }
    
    // Check for duplicate tags
    const uniqueTags = [...new Set(values)]
    if (uniqueTags.length !== values.length) {
      return 'Duplicate tags are not allowed'
    }
    
    // Check tag length
    for (const tag of values) {
      if (tag.length > 20) {
        return 'Tags must be 20 characters or less'
      }
    }
    
    return true
  },
}
```

## Custom Field Components

PayloadCMS allows you to replace any field's UI with custom React components:

### Custom Field Component

```typescript
// Field configuration
{
  name: 'colorPicker',
  type: 'text',
  required: true,
  admin: {
    components: {
      Field: '/components/ColorPickerField',
    },
  },
  validate: (value) => {
    const hexRegex = /^#([A-Fa-f0-9]{6}|[A-Fa-f0-9]{3})$/
    if (!hexRegex.test(value)) {
      return 'Must be a valid hex color code'
    }
    return true
  },
}
```

```typescript
// /components/ColorPickerField.tsx
'use client'
import React, { useState, useCallback } from 'react'
import { SketchPicker } from 'react-color'
import type { TextFieldClientProps } from 'payload'

export const ColorPickerField: React.FC<TextFieldClientProps> = ({
  field,
  value,
  setValue,
  errorMessage,
  readOnly,
}) => {
  const [showPicker, setShowPicker] = useState(false)
  
  const handleChange = useCallback((color: any) => {
    setValue(color.hex)
  }, [setValue])
  
  return (
    <div className="color-picker-field">
      <label className="field-label">
        {field.label}
        {field.required && <span className="required">*</span>}
      </label>
      
      <div className="color-picker-wrapper">
        <div 
          className="color-swatch"
          style={{ backgroundColor: value || '#ffffff' }}
          onClick={() => !readOnly && setShowPicker(!showPicker)}
        />
        
        <input
          type="text"
          value={value || ''}
          onChange={(e) => setValue(e.target.value)}
          readOnly={readOnly}
          placeholder="#ffffff"
          className="color-input"
        />
        
        {showPicker && !readOnly && (
          <div className="color-picker-popover">
            <div 
              className="color-picker-cover"
              onClick={() => setShowPicker(false)}
            />
            <SketchPicker
              color={value || '#ffffff'}
              onChange={handleChange}
              disableAlpha
            />
          </div>
        )}
      </div>
      
      {errorMessage && (
        <div className="field-error">{errorMessage}</div>
      )}
      
      {field.admin?.description && (
        <div className="field-description">
          {field.admin.description}
        </div>
      )}
    </div>
  )
}
```

### Custom Cell Component

```typescript
// Custom cell component for list view
// /components/ColorCell.tsx
export const ColorCell: React.FC<DefaultCellComponentProps> = ({
  cellData,
  rowData,
}) => {
  if (!cellData) return <span>—</span>
  
  return (
    <div className="color-cell">
      <div 
        className="color-swatch-small"
        style={{ backgroundColor: cellData }}
      />
      <span className="color-value">{cellData}</span>
    </div>
  )
}

// Field configuration
{
  name: 'brandColor',
  type: 'text',
  admin: {
    components: {
      Field: '/components/ColorPickerField',
      Cell: '/components/ColorCell',
    },
  },
}
```

### Complex Custom Field

```typescript
// Advanced custom field with multiple inputs
// Field configuration
{
  name: 'socialLinks',
  type: 'json',
  admin: {
    components: {
      Field: '/components/SocialLinksField',
    },
  },
}
```

```typescript
// /components/SocialLinksField.tsx
'use client'
import React, { useState, useCallback } from 'react'
import type { JSONFieldClientProps } from 'payload'

interface SocialLink {
  platform: string
  url: string
  icon?: string
}

const PLATFORMS = [
  { value: 'facebook', label: 'Facebook', icon: 'fab fa-facebook' },
  { value: 'twitter', label: 'Twitter', icon: 'fab fa-twitter' },
  { value: 'instagram', label: 'Instagram', icon: 'fab fa-instagram' },
  { value: 'linkedin', label: 'LinkedIn', icon: 'fab fa-linkedin' },
  { value: 'youtube', label: 'YouTube', icon: 'fab fa-youtube' },
]

export const SocialLinksField: React.FC<JSONFieldClientProps> = ({
  field,
  value,
  setValue,
  errorMessage,
  readOnly,
}) => {
  const socialLinks: SocialLink[] = value || []
  
  const addLink = useCallback(() => {
    const newLinks = [...socialLinks, { platform: '', url: '', icon: '' }]
    setValue(newLinks)
  }, [socialLinks, setValue])
  
  const removeLink = useCallback((index: number) => {
    const newLinks = socialLinks.filter((_, i) => i !== index)
    setValue(newLinks)
  }, [socialLinks, setValue])
  
  const updateLink = useCallback((index: number, field: keyof SocialLink, newValue: string) => {
    const newLinks = [...socialLinks]
    newLinks[index] = { ...newLinks[index], [field]: newValue }
    
    // Auto-set icon when platform changes
    if (field === 'platform') {
      const platform = PLATFORMS.find(p => p.value === newValue)
      if (platform) {
        newLinks[index].icon = platform.icon
      }
    }
    
    setValue(newLinks)
  }, [socialLinks, setValue])
  
  return (
    <div className="social-links-field">
      <label className="field-label">
        {field.label}
        {field.required && <span className="required">*</span>}
      </label>
      
      <div className="social-links-list">
        {socialLinks.map((link, index) => (
          <div key={index} className="social-link-item">
            <select
              value={link.platform}
              onChange={(e) => updateLink(index, 'platform', e.target.value)}
              disabled={readOnly}
              className="platform-select"
            >
              <option value="">Select platform</option>
              {PLATFORMS.map(platform => (
                <option key={platform.value} value={platform.value}>
                  {platform.label}
                </option>
              ))}
            </select>
            
            <input
              type="url"
              value={link.url}
              onChange={(e) => updateLink(index, 'url', e.target.value)}
              placeholder="https://..."
              disabled={readOnly}
              className="url-input"
            />
            
            <button
              type="button"
              onClick={() => removeLink(index)}
              disabled={readOnly}
              className="remove-link-btn"
            >
              Remove
            </button>
          </div>
        ))}
      </div>
      
      {!readOnly && (
        <button
          type="button"
          onClick={addLink}
          className="add-link-btn"
        >
          Add Social Link
        </button>
      )}
      
      {errorMessage && (
        <div className="field-error">{errorMessage}</div>
      )}
    </div>
  )
}
```

## Localization Support

PayloadCMS fields support comprehensive internationalization:

### Basic Localization

```typescript
// Localized text field
{
  name: 'title',
  type: 'text',
  required: true,
  localized: true, // Enable localization
  admin: {
    description: 'Title in multiple languages',
  },
}

// Localized rich text
{
  name: 'content',
  type: 'richText',
  localized: true,
  required: true,
}

// Localized array field
{
  name: 'features',
  type: 'array',
  localized: true,
  fields: [
    {
      name: 'title',
      type: 'text',
      required: true,
    },
    {
      name: 'description',
      type: 'textarea',
      required: true,
    },
  ],
}
```

### Conditional Localization

```typescript
{
  name: 'productName',
  type: 'text',
  required: true,
  localized: ({ req }) => {
    // Only localize for certain product types
    return req.data?.productType === 'international'
  },
}
```

### Fallback Locales

```typescript
// PayloadCMS configuration
export default buildConfig({
  localization: {
    locales: [
      {
        label: 'English',
        code: 'en',
      },
      {
        label: 'Spanish',
        code: 'es',
        fallbackLocale: 'en', // Fallback to English
      },
      {
        label: 'French',
        code: 'fr',
        fallbackLocale: 'en', // Fallback to English
      },
    ],
    defaultLocale: 'en',
  },
})
```

## Performance Optimization

### Field-Level Optimization

```typescript
// Indexed fields for better query performance
{
  name: 'slug',
  type: 'text',
  required: true,
  unique: true,
  index: true, // Add database index
}

// Conditional field loading
{
  name: 'heavyData',
  type: 'richText',
  admin: {
    condition: (data) => data.includeHeavyData === true,
  },
}

// Lazy loaded relationships
{
  name: 'relatedPosts',
  type: 'relationship',
  relationTo: 'posts',
  hasMany: true,
  admin: {
    description: 'Related posts (loaded on demand)',
    // Don't populate in list views
    hidden: ({ findMany }) => findMany,
  },
}
```

### Large Form Optimization

```typescript
// Use tabs to organize large forms
{
  name: 'productDetails',
  type: 'tabs',
  tabs: [
    {
      label: 'Basic Info',
      fields: [
        { name: 'title', type: 'text', required: true },
        { name: 'description', type: 'textarea' },
      ],
    },
    {
      label: 'Pricing',
      fields: [
        { name: 'price', type: 'number', required: true },
        { name: 'salePrice', type: 'number' },
      ],
    },
    {
      label: 'Media',
      fields: [
        {
          name: 'images',
          type: 'array',
          fields: [
            { name: 'image', type: 'upload', relationTo: 'media' },
          ],
        },
      ],
    },
  ],
}

// Collapsible sections for optional fields
{
  name: 'advancedOptions',
  type: 'collapsible',
  label: 'Advanced Options',
  admin: {
    initCollapsed: true, // Start collapsed
  },
  fields: [
    // Advanced fields here
  ],
}
```

## Testing Field Configurations

### Field Validation Testing

```typescript
import { text, email, number } from 'payload/fields/validations'

describe('Field Validations', () => {
  const mockReq = {
    payload: { config: {} },
    t: (key: string, vars?: any) => `${key}${vars ? JSON.stringify(vars) : ''}`,
  }
  
  describe('Text Field', () => {
    it('should validate required text', () => {
      const result = text('', { required: true, req: mockReq })
      expect(result).toBe('validation:required')
    })
    
    it('should validate text length', () => {
      const result = text('abc', { 
        minLength: 5, 
        required: false, 
        req: mockReq 
      })
      expect(result).toContain('validation:longerThanMin')
    })
    
    it('should validate text arrays', () => {
      const result = text(['a', 'b'], {
        hasMany: true,
        minRows: 3,
        req: mockReq,
      })
      expect(result).toContain('validation:tooFewArrayItems')
    })
  })
  
  describe('Email Field', () => {
    it('should validate email format', () => {
      const result = email('invalid-email', { req: mockReq })
      expect(result).toBe('validation:validEmail')
    })
    
    it('should accept valid email', () => {
      const result = email('test@example.com', { req: mockReq })
      expect(result).toBe(true)
    })
  })
  
  describe('Number Field', () => {
    it('should validate number range', () => {
      const result = number(150, { 
        min: 0, 
        max: 100, 
        req: mockReq 
      })
      expect(result).toContain('validation:lessThanMax')
    })
  })
})
```

### Custom Field Component Testing

```typescript
import { render, screen, fireEvent } from '@testing-library/react'
import { ColorPickerField } from '../components/ColorPickerField'

describe('ColorPickerField', () => {
  const mockField = {
    name: 'color',
    type: 'text' as const,
    label: 'Color',
    required: true,
  }
  
  const mockProps = {
    field: mockField,
    value: '#ffffff',
    setValue: jest.fn(),
    errorMessage: '',
    readOnly: false,
  }
  
  it('should render color swatch and input', () => {
    render(<ColorPickerField {...mockProps} />)
    
    expect(screen.getByRole('textbox')).toBeInTheDocument()
    expect(screen.getByText('Color')).toBeInTheDocument()
  })
  
  it('should call setValue when input changes', () => {
    render(<ColorPickerField {...mockProps} />)
    
    const input = screen.getByRole('textbox')
    fireEvent.change(input, { target: { value: '#ff0000' } })
    
    expect(mockProps.setValue).toHaveBeenCalledWith('#ff0000')
  })
  
  it('should display error message', () => {
    render(<ColorPickerField {...mockProps} errorMessage="Invalid color" />)
    
    expect(screen.getByText('Invalid color')).toBeInTheDocument()
  })
  
  it('should be read-only when specified', () => {
    render(<ColorPickerField {...mockProps} readOnly={true} />)
    
    const input = screen.getByRole('textbox')
    expect(input).toHaveAttribute('readOnly')
  })
})
```

## Troubleshooting

### Common Issues

#### "Field is required" Validation Error
**Problem:** Required field validation failing unexpectedly

**Solution:**
```typescript
// Check for proper field configuration
{
  name: 'title',
  type: 'text',
  required: true,
  validate: (value) => {
    console.log('Validating title:', value, typeof value)
    if (typeof value !== 'string' || value.trim() === '') {
      return 'Title is required and cannot be empty'
    }
    return true
  },
}

// For array fields, check minRows
{
  name: 'items',
  type: 'array',
  minRows: 1, // Ensures at least one item
  fields: [
    { name: 'name', type: 'text', required: true },
  ],
}
```

#### Custom Component Not Rendering
**Problem:** Custom field components not appearing in admin

**Solution:**
```typescript
// Ensure correct component path and export
{
  name: 'customField',
  type: 'text',
  admin: {
    components: {
      Field: '/components/CustomField', // Absolute path from project root
    },
  },
}

// Component must be properly exported
// /components/CustomField.tsx
'use client'
export const CustomField: React.FC<TextFieldClientProps> = (props) => {
  // Component implementation
}

// Default export also works
export default CustomField
```

#### Conditional Logic Not Working
**Problem:** Field conditions not showing/hiding fields properly

**Solution:**
```typescript
// Use correct condition syntax
{
  name: 'conditionalField',
  type: 'text',
  admin: {
    condition: (data, siblingData, { user }) => {
      // Debug the condition
      console.log('Condition data:', { data, siblingData, user })
      
      // Ensure you're checking the right data structure
      return data?.showConditional === true
    },
  },
}

// For fields within arrays/blocks, use siblingData
{
  name: 'items',
  type: 'array',
  fields: [
    {
      name: 'type',
      type: 'select',
      options: ['basic', 'advanced'],
    },
    {
      name: 'advancedOptions',
      type: 'text',
      admin: {
        condition: (data, siblingData) => {
          // siblingData is the current array item
          return siblingData?.type === 'advanced'
        },
      },
    },
  ],
}
```

#### Hook Execution Issues
**Problem:** Field hooks not executing or causing errors

**Solution:**
```typescript
// Proper hook implementation with error handling
{
  name: 'processedField',
  type: 'text',
  hooks: {
    beforeChange: [
      async ({ value, req }) => {
        try {
          // Always return a value
          if (!value) return value
          
          // Process the value
          const processed = await processValue(value, req)
          return processed
        } catch (error) {
          req.payload.logger.error('Field hook error:', error)
          // Return original value on error
          return value
        }
      },
    ],
  },
}

// Hook execution order matters
{
  name: 'chainedField',
  type: 'text',
  hooks: {
    beforeChange: [
      // First hook
      ({ value }) => {
        return value?.toLowerCase()
      },
      // Second hook (receives result of first)
      ({ value }) => {
        return value?.trim()
      },
    ],
  },
}
```

### Performance Issues

#### Slow Form Loading
**Problem:** Forms with many fields loading slowly

**Solution:**
```typescript
// Use tabs to split large forms
{
  name: 'contentTabs',
  type: 'tabs',
  tabs: [
    {
      label: 'Essential',
      fields: [
        // Only essential fields in first tab
      ],
    },
    {
      label: 'Additional',
      fields: [
        // Additional fields in second tab
      ],
    },
  ],
}

// Use collapsible fields for optional content
{
  name: 'optionalSettings',
  type: 'collapsible',
  label: 'Optional Settings',
  admin: {
    initCollapsed: true,
  },
  fields: [
    // Optional fields
  ],
}
```

#### Memory Issues with Large Arrays
**Problem:** Performance issues with large array fields

**Solution:**
```typescript
// Limit array size
{
  name: 'items',
  type: 'array',
  maxRows: 50, // Reasonable limit
  admin: {
    description: 'Maximum 50 items allowed',
  },
  fields: [
    // Array item fields
  ],
}

// Use pagination for large datasets
{
  name: 'relatedItems',
  type: 'relationship',
  relationTo: 'items',
  hasMany: true,
  admin: {
    pagination: {
      limit: 10,
    },
  },
}
```

## Migration Guide

### From v2 to v3

Key changes in the fields system:

```typescript
// v2 (Old syntax)
const field = {
  name: 'myField',
  type: 'text',
  // Old admin config
  admin: {
    components: {
      Field: MyCustomComponent,
    },
  },
  // Old hooks
  hooks: {
    beforeChange: [
      ({ data, req }) => {
        // Old hook signature
        return data
      },
    ],
  },
}

// v3 (New syntax)
const field: TextField = {
  name: 'myField',
  type: 'text',
  admin: {
    components: {
      Field: '/components/MyCustomComponent', // String path
    },
  },
  hooks: {
    beforeChange: [
      ({ value, data, req, operation }) => {
        // New hook signature with more context
        return value
      },
    ],
  },
}
```

### Component Migration

```typescript
// v2 Component
import React from 'react'

const OldComponent = ({ value, onChange }) => {
  return <input value={value} onChange={onChange} />
}

// v3 Component
'use client'
import React from 'react'
import type { TextFieldClientProps } from 'payload'

const NewComponent: React.FC<TextFieldClientProps> = ({
  field,
  value,
  setValue,
  errorMessage,
  readOnly,
}) => {
  return (
    <div>
      <label>{field.label}</label>
      <input 
        value={value || ''} 
        onChange={(e) => setValue(e.target.value)}
        readOnly={readOnly}
      />
      {errorMessage && <div className="error">{errorMessage}</div>}
    </div>
  )
}
```

## Example Projects

- [Field Customization Examples](https://github.com/payloadcms/payload/tree/main/examples/custom-components) - Custom field components and validation
- [E-commerce Product Fields](https://github.com/payloadcms/payload/tree/main/examples/ecommerce) - Complex product data structures
- [Blog Content Fields](https://github.com/payloadcms/payload/tree/main/examples/blog) - Rich content and media fields
- [Form Builder](https://github.com/payloadcms/payload/tree/main/examples/form-builder) - Dynamic form field generation

## Contributing

Found a bug or have a suggestion? [Open an issue](https://github.com/payloadcms/payload/issues) or submit a Pull Request.

## License

MIT License - see the [LICENSE](https://github.com/payloadcms/payload/blob/main/LICENSE) file for details.