---
title: UploadThing Storage for PayloadCMS
label: Storage UploadThing
order: 10
desc: PayloadCMS storage adapter for UploadThing - enabling secure file uploads with CDN delivery and client-side uploads
keywords: [payloadcms, uploadthing, storage, adapter, file-upload, cdn, client-uploads, media]
---

<Banner type="warning">
**Original Documentation**: The content below comes from the official PayloadCMS README.
Further in the document, you'll find an extended, more detailed version of this documentation.
</Banner>

# Uploadthing Storage for Payload (beta)

This package provides a way to use [uploadthing](https://uploadthing.com) with Payload.

## Installation

```sh
pnpm add @payloadcms/storage-uploadthing
```

## Usage

- Configure the `collections` object to specify which collections should use uploadthing. The slug _must_ match one of your existing collection slugs and be an `upload` type.
- Get an API key from Uploadthing and set it as `apiKey` in the `options` object.
- `acl` is optional and defaults to `public-read`.
- When deploying to Vercel, server uploads are limited with 4.5MB. Set `clientUploads` to `true` to do uploads directly on the client.

```ts
export default buildConfig({
  collections: [Media],
  plugins: [
    uploadthingStorage({
      collections: {
        media: true,
      },
      options: {
        token: process.env.UPLOADTHING_TOKEN,
        acl: 'public-read',
      },
    }),
  ],
})
```

---

## 📚 Extended Documentation

<Banner type="success">
**Note**: The documentation below has been automatically generated based on source code analysis and contains more detailed information than the original documentation above.
</Banner>

![NPM Version](https://img.shields.io/npm/v/@payloadcms/storage-uploadthing)
![Bundle Size](https://img.shields.io/bundlephobia/minzip/@payloadcms/storage-uploadthing)

## Detailed Overview

The `@payloadcms/storage-uploadthing` package is a PayloadCMS storage adapter that seamlessly integrates UploadThing's file storage service with your PayloadCMS application. This adapter provides enterprise-grade file storage with built-in CDN delivery, automatic optimizations, and support for both server-side and client-side uploads.

**Key benefits:**
- **CDN Integration**: Automatic global CDN distribution through UploadThing
- **Vercel Optimization**: Client-side uploads to bypass Vercel's 4.5MB server upload limits
- **Secure Access Control**: Configurable ACL (Access Control Lists) for public or private files
- **Automatic Cleanup**: Built-in file deletion when records are removed
- **Image Processing**: Automatic image optimization and resizing support

The adapter is designed for developers who need reliable, scalable file storage without the complexity of managing their own infrastructure, making it perfect for applications requiring efficient media handling and global content delivery.

<Banner type="info">
The package is open-source. [View source code](https://github.com/payloadcms/payload/tree/main/packages/storage-uploadthing). Need help? [Community Help](https://payloadcms.com/community-help).
</Banner>

## System Requirements

- **PayloadCMS**: 3.x or higher
- **Node.js**: ^18.20.2 || >=20.9.0
- **TypeScript**: 4.5+ (optional but recommended)
- **UploadThing Account**: Valid UploadThing token required

## Installation

```bash
# npm
npm install @payloadcms/storage-uploadthing

# yarn
yarn add @payloadcms/storage-uploadthing

# pnpm
pnpm add @payloadcms/storage-uploadthing
```

### Peer Dependencies
This package requires PayloadCMS as a peer dependency:
```bash
npm install payload@workspace:*
```

## Quick Start

Basic configuration for using UploadThing storage:

```typescript
import { uploadthingStorage } from '@payloadcms/storage-uploadthing'
import { buildConfig } from 'payload'

export default buildConfig({
  collections: [
    {
      slug: 'media',
      upload: true,
      fields: [],
    },
  ],
  plugins: [
    uploadthingStorage({
      collections: {
        media: true, // Enable UploadThing for the media collection
      },
      options: {
        token: process.env.UPLOADTHING_TOKEN, // Your UploadThing API token
        acl: 'public-read', // Default access control
      },
    }),
  ],
})
```

### Environment Variables
```bash
# Required: Your UploadThing API token
UPLOADTHING_TOKEN=your_uploadthing_token_here
```

## Detailed Configuration

### Main Options

#### `collections`

- **Type**: `Partial<Record<UploadCollectionSlug, Omit<CollectionOptions, 'adapter'> | true>>`
- **Default value**: None (required)
- **Required**: `true`

Specifies which PayloadCMS collections should use UploadThing storage. The collection slug must match an existing upload-enabled collection in your PayloadCMS configuration.

```typescript
uploadthingStorage({
  collections: {
    media: true, // Simple enablement
    documents: { // Advanced configuration
      disablePayloadAccessControl: false,
      prefix: 'docs/',
    },
  },
  options: {
    token: process.env.UPLOADTHING_TOKEN,
  },
})
```

#### `options`

- **Type**: `{ acl?: ACL } & UTApiOptions`
- **Default value**: `{ acl: 'public-read' }`
- **Required**: `true`

Core UploadThing configuration options including API credentials and access control settings.

```typescript
uploadthingStorage({
  collections: { media: true },
  options: {
    token: process.env.UPLOADTHING_TOKEN, // UploadThing API token
    acl: 'private', // 'public-read' | 'private'
    // Additional UTApiOptions can be added here
  },
})
```

##### Sub-options:
- `token` (string): UploadThing API token - **required**
- `acl` (ACL): Access control level - defaults to `'public-read'`

#### `clientUploads`

- **Type**: `{ access?: ClientUploadsAccess; routerInputConfig?: FileRouterInputConfig } | boolean`
- **Default value**: `false`
- **Required**: `false`

Enables direct client-side uploads, bypassing server limitations (especially useful for Vercel deployments with 4.5MB limits).

```typescript
uploadthingStorage({
  collections: { media: true },
  clientUploads: true, // Simple enablement
  // OR advanced configuration:
  clientUploads: {
    access: ({ req }) => Boolean(req.user), // Custom access control
    routerInputConfig: {
      blob: {
        maxFileSize: '10MB',
        maxFileCount: 5,
      },
    },
  },
  options: {
    token: process.env.UPLOADTHING_TOKEN,
  },
})
```

#### `enabled`

- **Type**: `boolean`
- **Default value**: `true`
- **Required**: `false`

Allows conditional enablement/disablement of the plugin, useful for different environments.

```typescript
uploadthingStorage({
  enabled: process.env.NODE_ENV === 'production',
  collections: { media: true },
  options: {
    token: process.env.UPLOADTHING_TOKEN,
  },
})
```

### Configuration Schema

```typescript
export type UploadthingStorageOptions = {
  /**
   * Do uploads directly on the client, to bypass limits on Vercel.
   */
  clientUploads?:
    | {
        access?: ClientUploadsAccess
        routerInputConfig?: FileRouterInputConfig
      }
    | boolean

  /**
   * Collection options to apply the adapter to.
   */
  collections: Partial<Record<UploadCollectionSlug, Omit<CollectionOptions, 'adapter'> | true>>

  /**
   * Whether or not to enable the plugin
   *
   * Default: true
   */
  enabled?: boolean

  /**
   * Uploadthing Options
   */
  options: {
    /**
     * @default 'public-read'
     */
    acl?: ACL
  } & UTApiOptions
}

export type ACL = 'private' | 'public-read'

export type FileRouterInputConfig = Parameters<ReturnType<typeof createUploadthing>>[0]
```

## Usage Guides

### Basic File Upload Configuration

Setting up a simple media collection with UploadThing storage:

```typescript
import { uploadthingStorage } from '@payloadcms/storage-uploadthing'

export default buildConfig({
  collections: [
    {
      slug: 'media',
      upload: {
        imageSizes: [
          {
            name: 'thumbnail',
            width: 300,
            height: 300,
            position: 'centre',
          },
          {
            name: 'hero',
            width: 1200,
            height: 600,
            position: 'centre',
          },
        ],
      },
      fields: [
        {
          name: 'alt',
          type: 'text',
          required: true,
        },
      ],
    },
  ],
  plugins: [
    uploadthingStorage({
      collections: {
        media: true,
      },
      options: {
        token: process.env.UPLOADTHING_TOKEN,
        acl: 'public-read',
      },
    }),
  ],
})
```

### Client-Side Uploads for Vercel

Enabling client-side uploads to bypass Vercel's server upload limitations:

```typescript
export default buildConfig({
  collections: [Media],
  plugins: [
    uploadthingStorage({
      collections: {
        media: true,
      },
      clientUploads: {
        access: ({ req }) => {
          // Only allow authenticated users to upload
          return Boolean(req.user)
        },
        routerInputConfig: {
          blob: {
            maxFileSize: '50MB', // Larger files possible with client uploads
            maxFileCount: 10,
          },
        },
      },
      options: {
        token: process.env.UPLOADTHING_TOKEN,
        acl: 'public-read',
      },
    }),
  ],
})
```

### Multiple Collections with Different ACLs

Configure different collections with varying access controls:

```typescript
export default buildConfig({
  collections: [MediaCollection, DocumentsCollection],
  plugins: [
    uploadthingStorage({
      collections: {
        media: true, // Public media files
      },
      options: {
        token: process.env.UPLOADTHING_TOKEN,
        acl: 'public-read',
      },
    }),
    // Separate plugin instance for private documents
    uploadthingStorage({
      collections: {
        documents: true, // Private document storage
      },
      options: {
        token: process.env.UPLOADTHING_TOKEN,
        acl: 'private',
      },
    }),
  ],
})
```

### Advanced Patterns

#### Environment-Conditional Configuration

```typescript
const isProduction = process.env.NODE_ENV === 'production'

export default buildConfig({
  collections: [Media],
  plugins: [
    uploadthingStorage({
      enabled: isProduction, // Only use UploadThing in production
      collections: {
        media: true,
      },
      clientUploads: isProduction, // Client uploads only in production
      options: {
        token: process.env.UPLOADTHING_TOKEN,
        acl: isProduction ? 'public-read' : 'private',
      },
    }),
  ],
})
```

## API Reference

### Functions

#### `uploadthingStorage(options)`

The main plugin function that configures UploadThing storage for PayloadCMS.

**Parameters:**
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `options` | `UploadthingStorageOptions` | Yes | Configuration options for the storage adapter |

**Returns:** `Plugin` - PayloadCMS plugin instance

**Example:**
```typescript
const plugin = uploadthingStorage({
  collections: { media: true },
  options: { token: 'your-token' },
})
```

### React Components

#### `UploadthingClientUploadHandler`

Client-side upload handler component for direct browser uploads.

**Props:**
| Prop | Type | Description |
|------|------|-------------|
| `apiRoute` | `string` | API route for upload handling |
| `collectionSlug` | `string` | Target collection slug |
| `file` | `File` | File object to upload |
| `serverHandlerPath` | `string` | Server handler endpoint path |
| `serverURL` | `string` | Base server URL |

**Example:**
```tsx
import { UploadthingClientUploadHandler } from '@payloadcms/storage-uploadthing/client'

// This component is used internally by PayloadCMS
// when clientUploads is enabled
```

### Internal Functions

#### `generateURL({ data, filename, prefix })`

Generates public URLs for uploaded files.

**Parameters:**
- `data`: Upload document data
- `filename`: Name of the file
- `prefix`: Optional URL prefix

**Returns:** `string` - Public URL for the file

**Example:**
```typescript
// Internal usage - generates URLs like:
// https://utfs.io/f/your-file-key
```

#### `getHandleUpload({ acl, utApi })`

Creates upload handler for server-side file processing.

**Parameters:**
- `acl`: Access control level
- `utApi`: UploadThing API instance

**Returns:** `HandleUpload` - Upload handler function

#### `getHandleDelete({ utApi })`

Creates deletion handler for file cleanup.

**Parameters:**
- `utApi`: UploadThing API instance

**Returns:** `HandleDelete` - Deletion handler function

### TypeScript Types

```typescript
// Main configuration type
export type UploadthingStorageOptions = {
  clientUploads?:
    | {
        access?: ClientUploadsAccess
        routerInputConfig?: FileRouterInputConfig
      }
    | boolean
  collections: Partial<Record<UploadCollectionSlug, Omit<CollectionOptions, 'adapter'> | true>>
  enabled?: boolean
  options: {
    acl?: ACL
  } & UTApiOptions
}

// Access Control List options
export type ACL = 'private' | 'public-read'

// File router configuration type
export type FileRouterInputConfig = Parameters<ReturnType<typeof createUploadthing>>[0]
```

## Integrations

### PayloadCMS Hooks
The adapter integrates with PayloadCMS lifecycle hooks:
- **beforeChange**: Handles file uploads before document creation/update
- **afterDelete**: Cleans up files when documents are deleted
- **afterChange**: Updates file metadata after successful uploads

### Database
The adapter adds a hidden `_key` field to upload collections to store UploadThing file keys:
```typescript
{
  name: '_key',
  type: 'text',
  admin: {
    hidden: true,
  },
}
```

### External Services
- **UploadThing CDN**: Automatic global content delivery
- **Image Processing**: Built-in optimization and resizing
- **Vercel Integration**: Optimized for Vercel deployments

## Troubleshooting

### Common Issues

#### Upload Fails with "Error uploading file" Message

**Problem:** Files fail to upload with generic error messages.

**Solution:**
1. Verify your UploadThing token is correct and has proper permissions
2. Check that your collection slug matches exactly
3. Ensure the collection has `upload: true` configured

**Example:**
```typescript
// Correct configuration
{
  slug: 'media', // Must match exactly in plugin config
  upload: true,  // Required for upload collections
}
```

#### Client Uploads Not Working

**Problem:** Client-side uploads are not functioning despite being enabled.

**Solution:**
1. Ensure you're using the correct client export path
2. Verify the access function permits the current user
3. Check browser console for JavaScript errors

**Example:**
```typescript
clientUploads: {
  access: ({ req }) => {
    console.log('User check:', req.user) // Debug access control
    return Boolean(req.user)
  },
}
```

#### Files Not Accessible After Upload

**Problem:** Uploaded files return 404 errors when accessed.

**Solution:**
1. Check the ACL setting matches your access requirements
2. Verify the UploadThing token has read permissions
3. Ensure the `_key` field is being saved correctly

**Example:**
```typescript
options: {
  token: process.env.UPLOADTHING_TOKEN,
  acl: 'public-read', // Must match your access needs
}
```

#### Vercel 4.5MB Upload Limit

**Problem:** Server uploads fail on Vercel with large files.

**Solution:**
Enable client-side uploads to bypass server limitations:

```typescript
uploadthingStorage({
  clientUploads: true, // Enable client-side uploads
  collections: { media: true },
  options: {
    token: process.env.UPLOADTHING_TOKEN,
  },
})
```

### Debugging

Enable PayloadCMS debug logging to troubleshoot upload issues:

```bash
DEBUG=payload:* npm run dev
```

Check UploadThing dashboard for detailed error logs and usage statistics.

## Performance

### Performance Optimization

1. **Use Client Uploads**: Reduce server load by enabling client-side uploads
2. **Configure Image Sizes**: Pre-generate required image sizes to avoid runtime processing
3. **Set Appropriate ACLs**: Use `public-read` for public content to enable CDN caching
4. **Monitor File Sizes**: Set reasonable `maxFileSize` limits to prevent abuse

```typescript
uploadthingStorage({
  clientUploads: {
    routerInputConfig: {
      blob: {
        maxFileSize: '10MB', // Reasonable limit
        maxFileCount: 1,     // Single file uploads
      },
    },
  },
  collections: {
    media: true,
  },
  options: {
    token: process.env.UPLOADTHING_TOKEN,
    acl: 'public-read', // Enable CDN caching
  },
})
```

## Security

**Security Best Practices:**

1. **Secure Token Storage**: Always use environment variables for UploadThing tokens
2. **Access Control**: Implement proper access control for client uploads
3. **File Type Validation**: Configure allowed file types in your collection settings
4. **Size Limits**: Set reasonable file size limits to prevent abuse

```typescript
uploadthingStorage({
  clientUploads: {
    access: ({ req, collectionSlug }) => {
      // Only allow authenticated admin users
      return req.user?.roles?.includes('admin')
    },
    routerInputConfig: {
      blob: {
        maxFileSize: '5MB',
        maxFileCount: 1,
      },
    },
  },
  collections: {
    media: true,
  },
  options: {
    token: process.env.UPLOADTHING_TOKEN, // Never hardcode tokens
    acl: 'private', // Use private ACL for sensitive content
  },
})
```

## Migration

### From version 3.53.x to 3.54.x

No breaking changes in this version. The package maintains backward compatibility with existing configurations.

## Contributing

Found a bug or have a suggestion? [Open an issue](https://github.com/payloadcms/payload/issues) or submit a Pull Request.

## License

MIT License - see [LICENSE.md](./LICENSE.md) for details.