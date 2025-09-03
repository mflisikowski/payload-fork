---
title: S3 Storage for Payload
label: Storage S3
order: 10
desc: Comprehensive AWS S3 storage adapter for PayloadCMS with client uploads, presigned URLs, and seamless integration.
keywords: [s3, amazon, aws, storage, upload, files, cloud, presigned, client-uploads, bucket]
---

<Banner type="warning">
**Original Documentation**: The content below comes from the official README.md of this package.
Further in the document, you'll find an extended, more detailed version of this documentation.
</Banner>

# S3 Storage for Payload

This package provides a simple way to use S3 with Payload.

**NOTE:** This package removes the need to use `@payloadcms/plugin-cloud-storage` as was needed in Payload 2.x.

## Installation

```sh
pnpm add @payloadcms/storage-s3
```

## Usage

- Configure the `collections` object to specify which collections should use the AWS S3 adapter. The slug _must_ match one of your existing collection slugs.
- The `config` object can be any [`S3ClientConfig`](https://docs.aws.amazon.com/AWSJavaScriptSDK/v3/latest/client/s3) object (from [`@aws-sdk/client-s3`](https://github.com/aws/aws-sdk-js-v3)). _This is highly dependent on your AWS setup_. Check the AWS documentation for more information.
- When enabled, this package will automatically set `disableLocalStorage` to `true` for each collection.
- When deploying to Vercel, server uploads are limited with 4.5MB. Set `clientUploads` to `true` to do uploads directly on the client. You must allow CORS PUT method for the bucket to your website.
- Configure `signedDownloads` (either globally of per-collection in `collections`) to use [presigned URLs](https://docs.aws.amazon.com/AmazonS3/latest/userguide/using-presigned-url.html) for files downloading. This can improve performance for large files (like videos) while still respecting your access control. Additionally, with `signedDownloads.shouldUseSignedURL` you can specify a condition whether Payload should use a presigned URL, if you want to use this feature only for specific files.

```ts
import { s3Storage } from '@payloadcms/storage-s3'
import { Media } from './collections/Media'
import { MediaWithPrefix } from './collections/MediaWithPrefix'

export default buildConfig({
  collections: [Media, MediaWithPrefix],
  plugins: [
    s3Storage({
      collections: {
        media: true,
        'media-with-prefix': {
          prefix,
        },
        'media-with-presigned-downloads': {
          // Filter only mp4 files
          signedDownloads: {
            shouldUseSignedURL: ({ collection, filename, req }) => {
              return filename.endsWith('.mp4')
            },
          },
        },
      },
      bucket: process.env.S3_BUCKET,
      config: {
        credentials: {
          accessKeyId: process.env.S3_ACCESS_KEY_ID,
          secretAccessKey: process.env.S3_SECRET_ACCESS_KEY,
        },
        region: process.env.S3_REGION,
        // ... Other S3 configuration
      },
    }),
  ],
})
```

### Configuration Options

See the the [AWS SDK Package](https://github.com/aws/aws-sdk-js-v3) and [`S3ClientConfig`](https://docs.aws.amazon.com/AWSJavaScriptSDK/v3/latest/client/s3) object for guidance on AWS S3 configuration.

---

## 📚 Extended Documentation

<Banner type="success">
**Note**: The documentation below has been automatically generated based on source code analysis and contains more detailed information than the original documentation above.
</Banner>

![NPM Version](https://img.shields.io/npm/v/@payloadcms/storage-s3)
![Bundle Size](https://img.shields.io/bundlephobia/minzip/@payloadcms/storage-s3)

## Detailed Overview

The `@payloadcms/storage-s3` package is a comprehensive storage adapter that enables PayloadCMS to seamlessly integrate with Amazon S3 and S3-compatible storage services. This package eliminates the need for the previous `@payloadcms/plugin-cloud-storage` approach used in Payload 2.x and provides modern, efficient file handling with advanced features.

Key capabilities include:
- **Automatic multipart uploads** for large files (>50MB) with optimized chunking and parallel processing
- **Client-side uploads** to bypass server limitations, especially useful for Vercel deployments
- **Presigned URL support** for secure, temporary file access without exposing credentials
- **Flexible file organization** with customizable prefixes per collection
- **Smart caching and streaming** with proper HTTP headers and ETags for optimal performance

The package is designed for developers building applications that require scalable file storage, content management systems, and applications with significant media handling requirements.

<Banner type="info">
The package is open-source. [View source code](https://github.com/payloadcms/payload/tree/main/packages/storage-s3). Need help? [Community Help](https://payloadcms.com/community-help).
</Banner>

## System Requirements

- **PayloadCMS**: ^3.0.0 (workspace dependency)
- **Node.js**: ^18.20.2 || >=20.9.0
- **TypeScript**: Supported with full type definitions
- **AWS SDK**: Uses AWS SDK v3 for optimal performance and modern API

### Additional Requirements
- **S3 Bucket**: Valid AWS S3 bucket or S3-compatible storage service
- **AWS Credentials**: Access key ID and secret access key with appropriate permissions
- **CORS Configuration**: Required for client-side uploads (if using `clientUploads`)

## Installation

```bash
# npm
npm install @payloadcms/storage-s3

# yarn
yarn add @payloadcms/storage-s3

# pnpm
pnpm add @payloadcms/storage-s3
```

### Peer Dependencies
This package requires the following peer dependencies:
```bash
# Payload CMS core
payload: workspace:*
```

### Core Dependencies
The package automatically installs:
```bash
@aws-sdk/client-s3: ^3.614.0
@aws-sdk/lib-storage: ^3.614.0  
@aws-sdk/s3-request-presigner: ^3.614.0
@payloadcms/plugin-cloud-storage: workspace:*
```

## Quick Start

Basic configuration for immediate use:

```typescript
import { s3Storage } from '@payloadcms/storage-s3'
import { buildConfig } from 'payload'

export default buildConfig({
  collections: [
    {
      slug: 'media',
      upload: true,
      fields: [
        {
          name: 'alt',
          type: 'text',
          required: true,
        }
      ]
    }
  ],
  plugins: [
    s3Storage({
      // Required: specify which collections use S3
      collections: {
        media: true, // Enable for 'media' collection
      },
      // Required: S3 bucket name
      bucket: process.env.S3_BUCKET!,
      // Required: AWS SDK configuration
      config: {
        credentials: {
          accessKeyId: process.env.S3_ACCESS_KEY_ID!,
          secretAccessKey: process.env.S3_SECRET_ACCESS_KEY!,
        },
        region: process.env.S3_REGION || 'us-east-1',
      },
    }),
  ],
})
```

### Environment Variables
```bash
# Required environment variables
S3_BUCKET=your-bucket-name
S3_ACCESS_KEY_ID=your-access-key-id
S3_SECRET_ACCESS_KEY=your-secret-access-key
S3_REGION=us-east-1

# Optional: for custom endpoints (e.g., MinIO, DigitalOcean Spaces)
S3_ENDPOINT=https://your-custom-endpoint.com
```

## Detailed Configuration

### Main Options

#### `collections`

- **Type**: `Partial<Record<UploadCollectionSlug, CollectionOptions | true>>`
- **Default value**: None
- **Required**: true

Defines which PayloadCMS upload collections should use the S3 adapter. The key must match an existing collection slug exactly.

```typescript
// Simple enablement
collections: {
  media: true,
  documents: true
}

// Advanced per-collection configuration
collections: {
  media: {
    prefix: 'uploads/images',
    signedDownloads: {
      expiresIn: 3600, // 1 hour
      shouldUseSignedURL: ({ filename }) => filename.endsWith('.mp4')
    }
  },
  documents: {
    prefix: 'documents',
    signedDownloads: true
  }
}
```

#### `bucket`

- **Type**: `string`
- **Default value**: None
- **Required**: true

The S3 bucket name where files will be stored. Must follow [AWS S3 bucket naming conventions](https://docs.aws.amazon.com/AmazonS3/latest/userguide/bucketnamingrules.html).

```typescript
bucket: 'my-app-production-files'
```

#### `config`

- **Type**: `AWS.S3ClientConfig`
- **Default value**: None
- **Required**: true

AWS SDK configuration object. This is highly dependent on your AWS setup and can include any valid S3ClientConfig options.

```typescript
config: {
  credentials: {
    accessKeyId: process.env.S3_ACCESS_KEY_ID,
    secretAccessKey: process.env.S3_SECRET_ACCESS_KEY,
  },
  region: 'us-west-2',
  endpoint: 'https://s3.us-west-2.amazonaws.com', // Optional: custom endpoint
  forcePathStyle: false, // Set to true for MinIO/custom endpoints
}
```

#### `acl`

- **Type**: `'private' | 'public-read'`
- **Default value**: undefined (uses bucket default)
- **Required**: false

Access Control List setting for uploaded files. Controls whether files are publicly accessible.

```typescript
// Make files publicly readable
acl: 'public-read'

// Keep files private (default)
acl: 'private'
```

#### `clientUploads`

- **Type**: `ClientUploadsConfig | boolean`
- **Default value**: false
- **Required**: false

Enables client-side uploads to bypass server limitations (especially useful for Vercel's 4.5MB limit).

```typescript
// Simple enablement
clientUploads: true

// Advanced configuration with access control
clientUploads: {
  access: ({ req, collectionSlug }) => {
    // Only allow authenticated users
    return Boolean(req.user)
  }
}
```

**Note**: Requires CORS configuration on your S3 bucket to allow PUT requests from your domain.

#### `signedDownloads`

- **Type**: `SignedDownloadsConfig | boolean`
- **Default value**: false
- **Required**: false

Configure presigned URLs for file downloads. Improves performance for large files while maintaining access control.

```typescript
// Simple enablement (7200 seconds / 2 hours default)
signedDownloads: true

// Advanced configuration
signedDownloads: {
  expiresIn: 3600, // 1 hour
  shouldUseSignedURL: ({ collection, filename, req }) => {
    // Only use for video files
    return filename.endsWith('.mp4') || filename.endsWith('.mov')
  }
}
```

#### `disableLocalStorage`

- **Type**: `boolean`
- **Default value**: true
- **Required**: false

Whether to disable local storage for collections using S3. Automatically set to `true` when the plugin is enabled.

#### `enabled`

- **Type**: `boolean`
- **Default value**: true
- **Required**: false

Whether the plugin is enabled. Useful for conditional enablement based on environment.

```typescript
enabled: process.env.NODE_ENV === 'production'
```

### Configuration Schema

```typescript
export type S3StorageOptions = {
  /** Access control list for uploaded files */
  acl?: 'private' | 'public-read'
  
  /** Bucket name following AWS S3 naming conventions */
  bucket: string
  
  /** Enable client-side uploads with optional access control */
  clientUploads?: ClientUploadsConfig | boolean
  
  /** Collection-specific configurations */
  collections: Partial<
    Record<
      UploadCollectionSlug,
      | ({
          signedDownloads?: SignedDownloadsConfig
        } & Omit<CollectionOptions, 'adapter'>)
      | true
    >
  >
  
  /** AWS S3 client configuration */
  config: AWS.S3ClientConfig
  
  /** Disable local storage (default: true) */
  disableLocalStorage?: boolean
  
  /** Enable/disable the plugin (default: true) */
  enabled?: boolean
  
  /** Global signed downloads configuration */
  signedDownloads?: SignedDownloadsConfig
}

export type SignedDownloadsConfig =
  | {
      /** Expiration time in seconds (default: 7200) */
      expiresIn?: number
      /** Conditional function to determine if signed URL should be used */
      shouldUseSignedURL?(args: {
        collection: CollectionConfig
        filename: string
        req: PayloadRequest
      }): boolean | Promise<boolean>
    }
  | boolean
```

## Usage Guides

### Basic File Upload Setup

Step-by-step guide for setting up basic file uploads:

```typescript
// 1. Define your media collection
const Media = {
  slug: 'media',
  upload: {
    staticDir: 'media', // Not used with S3, but required for type checking
    staticURL: '/media',
    imageSizes: [
      {
        name: 'thumbnail',
        width: 400,
        height: 300,
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
}

// 2. Configure the plugin
export default buildConfig({
  collections: [Media],
  plugins: [
    s3Storage({
      collections: {
        media: true,
      },
      bucket: process.env.S3_BUCKET,
      config: {
        credentials: {
          accessKeyId: process.env.S3_ACCESS_KEY_ID,
          secretAccessKey: process.env.S3_SECRET_ACCESS_KEY,
        },
        region: process.env.S3_REGION,
      },
    }),
  ],
})
```

### Advanced Multi-Collection Setup

Configure different storage strategies for different file types:

```typescript
export default buildConfig({
  collections: [Images, Documents, Videos],
  plugins: [
    s3Storage({
      collections: {
        // Images: public access, organized by date
        images: {
          prefix: `images/${new Date().getFullYear()}/${new Date().getMonth() + 1}`,
        },
        
        // Documents: private with signed downloads
        documents: {
          prefix: 'documents/private',
          signedDownloads: {
            expiresIn: 1800, // 30 minutes
            shouldUseSignedURL: () => true, // Always use signed URLs
          },
        },
        
        // Videos: client uploads for large files
        videos: {
          prefix: 'videos',
          signedDownloads: {
            expiresIn: 7200, // 2 hours
            shouldUseSignedURL: ({ filename, req }) => {
              // Use signed URLs for premium content
              return req.user?.role === 'premium'
            },
          },
        },
      },
      bucket: process.env.S3_BUCKET,
      acl: 'public-read',
      clientUploads: {
        access: ({ collectionSlug, req }) => {
          // Allow client uploads only for videos and authenticated users
          return collectionSlug === 'videos' && Boolean(req.user)
        },
      },
      config: {
        credentials: {
          accessKeyId: process.env.S3_ACCESS_KEY_ID,
          secretAccessKey: process.env.S3_SECRET_ACCESS_KEY,
        },
        region: process.env.S3_REGION,
      },
    }),
  ],
})
```

### Advanced Patterns

#### Custom S3-Compatible Storage (MinIO, DigitalOcean Spaces)

```typescript
s3Storage({
  collections: { media: true },
  bucket: 'my-space',
  config: {
    credentials: {
      accessKeyId: process.env.SPACES_ACCESS_KEY_ID,
      secretAccessKey: process.env.SPACES_SECRET_ACCESS_KEY,
    },
    endpoint: 'https://nyc3.digitaloceanspaces.com',
    region: 'nyc3',
    forcePathStyle: false, // DigitalOcean Spaces uses virtual-hosted style
  },
})
```

#### Dynamic File Organization

```typescript
s3Storage({
  collections: {
    media: {
      prefix: ({ req }) => {
        const userId = req.user?.id || 'anonymous'
        const date = new Date().toISOString().split('T')[0]
        return `uploads/${userId}/${date}`
      },
    },
  },
  bucket: process.env.S3_BUCKET,
  config: { /* ... */ },
})
```

## API Reference

### Functions

#### `s3Storage(options: S3StorageOptions): Plugin`

Main plugin function that creates the S3 storage adapter.

**Parameters:**
| Parameter | Type | Description |
|-----------|------|-------------|
| options | `S3StorageOptions` | Configuration object for S3 storage |

**Returns:** `Plugin` - PayloadCMS plugin instance

**Example:**
```typescript
const s3Plugin = s3Storage({
  collections: { media: true },
  bucket: 'my-bucket',
  config: { /* AWS config */ },
})
```

#### `getGenerateURL({ bucket, config }): GenerateURL`

Generates public URLs for stored files.

**Parameters:**
| Parameter | Type | Description |
|-----------|------|-------------|
| bucket | `string` | S3 bucket name |
| config | `AWS.S3ClientConfig` | S3 client configuration |

**Returns:** Function that generates URLs from filename and prefix

**Example:**
```typescript
const generateURL = getGenerateURL({
  bucket: 'my-bucket',
  config: { endpoint: 'https://s3.amazonaws.com' }
})
const url = generateURL({ filename: 'image.jpg', prefix: 'uploads' })
// Returns: "https://s3.amazonaws.com/my-bucket/uploads/image.jpg"
```

#### `getHandleUpload(args): HandleUpload`

Creates upload handler with automatic multipart upload for large files.

**Parameters:**
| Parameter | Type | Description |
|-----------|------|-------------|
| acl | `'private' \| 'public-read'` | Access control setting |
| bucket | `string` | S3 bucket name |
| getStorageClient | `() => AWS.S3` | Function to get S3 client |
| prefix | `string` | File prefix/path |

**Returns:** Upload handler function

**Example:**
```typescript
const handleUpload = getHandleUpload({
  bucket: 'my-bucket',
  getStorageClient: () => s3Client,
  prefix: 'uploads/',
  acl: 'public-read'
})
```

### React Components

#### `S3ClientUploadHandler`

Client-side upload handler component for browser-based file uploads.

**Usage:**
This component is automatically configured when `clientUploads` is enabled. It handles:
- Generating presigned URLs for upload
- Performing direct browser-to-S3 uploads
- Error handling and progress tracking

**Example:**
```typescript
// Automatically used when clientUploads is enabled
clientUploads: true
// The S3ClientUploadHandler is imported from '@payloadcms/storage-s3/client'
```

### TypeScript Types

```typescript
// Main configuration interface
export interface S3StorageOptions {
  acl?: 'private' | 'public-read'
  bucket: string
  clientUploads?: ClientUploadsConfig | boolean
  collections: Partial<Record<UploadCollectionSlug, CollectionOptions | true>>
  config: AWS.S3ClientConfig
  disableLocalStorage?: boolean
  enabled?: boolean
  signedDownloads?: SignedDownloadsConfig
}

// Signed downloads configuration
export type SignedDownloadsConfig =
  | {
      expiresIn?: number
      shouldUseSignedURL?(args: {
        collection: CollectionConfig
        filename: string
        req: PayloadRequest
      }): boolean | Promise<boolean>
    }
  | boolean

// Upload handler interface
export interface HandleUpload {
  (args: {
    data: Record<string, any>
    file: {
      buffer: Buffer
      filename: string
      mimeType: string
      tempFilePath?: string
    }
  }): Promise<Record<string, any>>
}

// URL generation interface
export interface GenerateURL {
  (args: {
    filename: string
    prefix?: string
  }): string
}
```

## Integrations

### PayloadCMS Hooks
The package automatically integrates with PayloadCMS lifecycle hooks:

- **Upload hooks**: Handles file processing during upload operations
- **Delete hooks**: Removes files from S3 when documents are deleted
- **Access control**: Respects PayloadCMS access control patterns
- **Validation hooks**: Validates file types and sizes according to collection configuration

### Database
The package doesn't require additional database schema changes. It stores:

- **File metadata** in existing PayloadCMS upload fields
- **S3 URLs** are generated dynamically 
- **Prefix information** for file organization
- **ETags** for caching and conditional requests

### External Services

#### Amazon S3
- **Primary integration** with full AWS S3 API support
- **IAM permissions** required: `s3:GetObject`, `s3:PutObject`, `s3:DeleteObject`
- **Bucket policies** for CORS configuration when using client uploads

#### S3-Compatible Services
- **MinIO**: Self-hosted S3-compatible storage
- **DigitalOcean Spaces**: Managed S3-compatible storage
- **Backblaze B2**: With S3-compatible API
- **Cloudflare R2**: Zero-egress S3-compatible storage

## Troubleshooting

### Common Issues

#### Files Not Uploading - CORS Configuration

**Problem:** Client uploads fail with CORS errors

**Solution:**
Configure your S3 bucket's CORS policy to allow PUT requests:

```json
[
  {
    "AllowedHeaders": ["*"],
    "AllowedMethods": ["GET", "PUT", "POST", "DELETE"],
    "AllowedOrigins": ["https://yourdomain.com"],
    "ExposeHeaders": ["ETag"],
    "MaxAgeSeconds": 3000
  }
]
```

**Example:**
```bash
# Using AWS CLI
aws s3api put-bucket-cors --bucket your-bucket-name --cors-configuration file://cors.json
```

#### Large File Upload Failures

**Problem:** Files over 50MB fail to upload or timeout

**Solution:**
The package automatically uses multipart uploads for files >50MB. Ensure your AWS credentials have `s3:PutObject` and `s3:AbortMultipartUpload` permissions.

```typescript
// Multipart upload configuration is handled automatically
// No additional configuration needed
```

#### Presigned URL Access Denied

**Problem:** Presigned URLs return 403 Access Denied

**Solution:**
Verify IAM permissions and bucket policies:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "s3:GetObject",
        "s3:PutObject",
        "s3:DeleteObject"
      ],
      "Resource": "arn:aws:s3:::your-bucket-name/*"
    }
  ]
}
```

#### Custom Endpoint Connection Issues

**Problem:** Cannot connect to MinIO or other S3-compatible services

**Solution:**
Configure `forcePathStyle` and ensure endpoint is correct:

```typescript
config: {
  endpoint: 'http://localhost:9000', // MinIO default
  forcePathStyle: true, // Required for MinIO
  region: 'us-east-1', // Required even for MinIO
  credentials: {
    accessKeyId: 'minioadmin',
    secretAccessKey: 'minioadmin',
  },
}
```

#### Image Resizing Not Working

**Problem:** PayloadCMS image resizing fails with S3 storage

**Solution:**
Ensure the `staticHandler` is properly configured and accessible:

```typescript
// The package handles this automatically
// Verify your collection upload configuration
upload: {
  imageSizes: [
    {
      name: 'thumbnail',
      width: 400,
      height: 300,
    }
  ]
}
```

### Debugging

Enable debug logging to troubleshoot issues:

```typescript
// Add to your payload.config.ts
export default buildConfig({
  logger: {
    level: 'debug', // Enable debug logging
  },
  // ... rest of config
})
```

Check S3 client configuration:
```typescript
// Test S3 connection
import { S3 } from '@aws-sdk/client-s3'

const client = new S3({
  credentials: {
    accessKeyId: process.env.S3_ACCESS_KEY_ID,
    secretAccessKey: process.env.S3_SECRET_ACCESS_KEY,
  },
  region: process.env.S3_REGION,
})

// Test bucket access
try {
  await client.headBucket({ Bucket: process.env.S3_BUCKET })
  console.log('S3 connection successful')
} catch (error) {
  console.error('S3 connection failed:', error)
}
```

## Performance

### Performance Optimization

**Multipart Uploads**: Files larger than 50MB automatically use multipart uploads with 4 parallel connections for optimal throughput.

**Client-Side Uploads**: Enable `clientUploads` to bypass server limitations and reduce server load:
```typescript
clientUploads: true // Recommended for production
```

**Presigned URLs**: Use for large file downloads to reduce server bandwidth:
```typescript
signedDownloads: {
  shouldUseSignedURL: ({ filename }) => {
    // Use for files larger than 10MB
    return filename.includes('large') || filename.endsWith('.mp4')
  }
}
```

**Connection Pooling**: The package automatically configures HTTP agent pooling:
```typescript
// Automatically configured - no action needed
const defaultRequestHandlerOpts = {
  httpAgent: {
    keepAlive: true,
    maxSockets: 100,
  },
}
```

**Caching Headers**: Automatic ETag and caching header management for optimal client-side caching.

## Security

**Access Control**: Always use IAM roles with minimal required permissions:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "s3:GetObject",
        "s3:PutObject", 
        "s3:DeleteObject"
      ],
      "Resource": "arn:aws:s3:::your-bucket-name/*"
    }
  ]
}
```

**Environment Variables**: Never commit AWS credentials to version control. Use environment variables or IAM roles.

**CORS Configuration**: Restrict CORS origins to your specific domains:
```json
{
  "AllowedOrigins": ["https://yourdomain.com", "https://admin.yourdomain.com"]
}
```

**Presigned URL Expiration**: Keep expiration times as short as practical:
```typescript
signedDownloads: {
  expiresIn: 1800, // 30 minutes max for sensitive content
}
```

## Migration

### From @payloadcms/plugin-cloud-storage (Payload 2.x)

The new S3 storage plugin simplifies configuration significantly:

**Before (Payload 2.x):**
```typescript
plugins: [
  cloudStorage({
    collections: {
      media: {
        adapter: s3Adapter({
          config: { /* ... */ },
          bucket: 'my-bucket',
        }),
      },
    },
  }),
]
```

**After (Payload 3.x):**
```typescript
plugins: [
  s3Storage({
    collections: {
      media: true,
    },
    bucket: 'my-bucket',
    config: { /* ... */ },
  }),
]
```

**Breaking Changes:**
- Remove `@payloadcms/plugin-cloud-storage` dependency
- Update plugin configuration syntax
- Collections automatically get `disableLocalStorage: true`
- Client uploads configuration syntax changed

## Contributing

Found a bug or have a suggestion? [Open an issue](https://github.com/payloadcms/payload/issues) or submit a Pull Request.

### Development Setup
```bash
# Clone the repository
git clone https://github.com/payloadcms/payload.git
cd payload/packages/storage-s3

# Install dependencies
pnpm install

# Build the package
pnpm build

# Run tests (if available)
pnpm test
```

## License

This package is licensed under the MIT License. See the [LICENSE.md](LICENSE.md) file for details.

Copyright (c) 2024 Payload. All rights reserved.