---
title: Google Cloud Storage for Payload
label: Storage GCS
order: 11
desc: Comprehensive Google Cloud Storage adapter for PayloadCMS with client uploads, signed URLs, and seamless integration.
keywords: [gcs, google-cloud, storage, upload, files, cloud, signed-urls, client-uploads, bucket]
---

<Banner type="warning">
**Original Documentation**: The content below comes from the official README.md of this package.
Further in the document, you'll find an extended, more detailed version of this documentation.
</Banner>

# Google Cloud Storage for Payload

This package provides a simple way to use [Google Cloud Storage](https://cloud.google.com/storage) with Payload.

**NOTE:** This package removes the need to use `@payloadcms/plugin-cloud-storage` as was needed in Payload 2.x.

## Installation

```sh
pnpm add @payloadcms/storage-gcs
```

## Usage

- Configure the `collections` object to specify which collections should use the Google Cloud Storage adapter. The slug _must_ match one of your existing collection slugs.
- When enabled, this package will automatically set `disableLocalStorage` to `true` for each collection.
- When deploying to Vercel, server uploads are limited with 4.5MB. Set `clientUploads` to `true` to do uploads directly on the client. You must allow CORS PUT method for the bucket to your website.

```ts
import { gcsStorage } from '@payloadcms/storage-gcs'
import { Media } from './collections/Media'
import { MediaWithPrefix } from './collections/MediaWithPrefix'

export default buildConfig({
  collections: [Media, MediaWithPrefix],
  plugins: [
    gcsStorage({
      collections: {
        media: true,
        'media-with-prefix': {
          prefix,
        },
      },
      bucket: process.env.GCS_BUCKET,
      options: {
        apiEndpoint: process.env.GCS_ENDPOINT,
        projectId: process.env.GCS_PROJECT_ID,
      },
    }),
  ],
})
```

### Configuration Options

| Option        | Description                                                                                         | Default   |
| ------------- | --------------------------------------------------------------------------------------------------- | --------- |
| `enabled`     | Whether or not to enable the plugin                                                                 | `true`    |
| `collections` | Collections to apply the storage to                                                                 |           |
| `bucket`      | The name of the bucket to use                                                                       |           |
| `options`     | Google Cloud Storage client configuration. See [Docs](https://github.com/googleapis/nodejs-storage) |           |
| `acl`         | Access control list for files that are uploaded                                                     | `Private` |

---

## 📚 Extended Documentation

<Banner type="success">
**Note**: The documentation below has been automatically generated based on source code analysis and contains more detailed information than the original documentation above.
</Banner>

![NPM Version](https://img.shields.io/npm/v/@payloadcms/storage-gcs)
![Bundle Size](https://img.shields.io/bundlephobia/minzip/@payloadcms/storage-gcs)

## Detailed Overview

The `@payloadcms/storage-gcs` package is a comprehensive storage adapter that enables PayloadCMS to seamlessly integrate with Google Cloud Storage (GCS). This package modernizes file storage by eliminating the need for the previous `@payloadcms/plugin-cloud-storage` approach used in Payload 2.x and provides efficient, scalable file handling with advanced cloud storage features.

Key capabilities include:
- **Native Google Cloud Storage integration** with full API support and automatic client management
- **Client-side uploads** to bypass server limitations, particularly beneficial for Vercel deployments
- **Signed URL generation** for secure, temporary file access without exposing credentials
- **Flexible file organization** with customizable prefixes per collection
- **Automatic stream handling** with proper HTTP headers and ETags for optimal performance
- **Built-in error handling** for cloud storage specific scenarios

The package is designed for developers building applications that require enterprise-grade file storage, content management systems, and applications with significant media handling requirements. It's particularly well-suited for organizations already using Google Cloud Platform services.

<Banner type="info">
The package is open-source. [View source code](https://github.com/payloadcms/payload/tree/main/packages/storage-gcs). Need help? [Community Help](https://payloadcms.com/community-help).
</Banner>

## System Requirements

- **PayloadCMS**: ^3.0.0 (workspace dependency)
- **Node.js**: ^18.20.2 || >=20.9.0
- **TypeScript**: Supported with full type definitions
- **Google Cloud SDK**: Uses @google-cloud/storage v7.7.0+ for optimal performance

### Additional Requirements
- **Google Cloud Project**: Valid GCP project with Cloud Storage API enabled
- **Service Account**: GCS service account credentials with appropriate permissions
- **Storage Bucket**: Pre-created Google Cloud Storage bucket
- **CORS Configuration**: Required for client-side uploads (if using `clientUploads`)

## Installation

```bash
# npm
npm install @payloadcms/storage-gcs

# yarn
yarn add @payloadcms/storage-gcs

# pnpm
pnpm add @payloadcms/storage-gcs
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
@google-cloud/storage: ^7.7.0
@payloadcms/plugin-cloud-storage: workspace:*
```

## Quick Start

Basic configuration for immediate use:

```typescript
import { gcsStorage } from '@payloadcms/storage-gcs'
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
    gcsStorage({
      // Required: specify which collections use GCS
      collections: {
        media: true, // Enable for 'media' collection
      },
      // Required: GCS bucket name
      bucket: process.env.GCS_BUCKET!,
      // Required: Google Cloud Storage configuration
      options: {
        projectId: process.env.GCS_PROJECT_ID!,
        keyFilename: process.env.GCS_KEY_FILE, // Path to service account key
        // Or use credentials object
        credentials: {
          client_email: process.env.GCS_CLIENT_EMAIL!,
          private_key: process.env.GCS_PRIVATE_KEY!.replace(/\\n/g, '\n'),
        },
      },
    }),
  ],
})
```

### Environment Variables
```bash
# Required environment variables
GCS_BUCKET=your-bucket-name
GCS_PROJECT_ID=your-gcp-project-id

# Option 1: Service account key file
GCS_KEY_FILE=./path/to/service-account-key.json

# Option 2: Service account credentials (for serverless)
GCS_CLIENT_EMAIL=your-service-account@your-project.iam.gserviceaccount.com
GCS_PRIVATE_KEY="-----BEGIN PRIVATE KEY-----\n...\n-----END PRIVATE KEY-----\n"

# Optional: Custom endpoint (for development/testing)
GCS_ENDPOINT=http://localhost:4443
```

## Detailed Configuration

### Main Options

#### `collections`

- **Type**: `Partial<Record<UploadCollectionSlug, CollectionOptions | true>>`
- **Default value**: None
- **Required**: true

Defines which PayloadCMS upload collections should use the GCS adapter. The key must match an existing collection slug exactly.

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
  },
  documents: {
    prefix: 'documents/private',
  }
}
```

#### `bucket`

- **Type**: `string`
- **Default value**: None
- **Required**: true

The Google Cloud Storage bucket name where files will be stored. The bucket must already exist in your GCP project.

```typescript
bucket: 'my-app-production-files'
```

#### `options`

- **Type**: `StorageOptions` (from @google-cloud/storage)
- **Default value**: None
- **Required**: true

Google Cloud Storage client configuration object. This follows the standard Google Cloud SDK configuration.

```typescript
options: {
  projectId: 'my-gcp-project',
  keyFilename: './service-account-key.json', // Local development
  // OR for serverless/production
  credentials: {
    client_email: process.env.GCS_CLIENT_EMAIL,
    private_key: process.env.GCS_PRIVATE_KEY.replace(/\\n/g, '\n'),
  },
  // Optional: custom endpoint for testing
  apiEndpoint: 'http://localhost:4443',
}
```

#### `acl`

- **Type**: `'Private' | 'Public'`
- **Default value**: undefined (uses bucket default)
- **Required**: false

Access Control List setting for uploaded files. Controls whether files are publicly accessible.

```typescript
// Make files publicly readable
acl: 'Public'

// Keep files private (default)
acl: 'Private'
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

**Note**: Requires CORS configuration on your GCS bucket to allow PUT requests from your domain.

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
export interface GcsStorageOptions {
  /** Access control list for uploaded files */
  acl?: 'Private' | 'Public'
  
  /** The name of the bucket to use */
  bucket: string
  
  /** Enable client-side uploads with optional access control */
  clientUploads?: ClientUploadsConfig
  
  /** Collection-specific configurations */
  collections: Partial<Record<UploadCollectionSlug, Omit<CollectionOptions, 'adapter'> | true>>
  
  /** Enable/disable the plugin (default: true) */
  enabled?: boolean
  
  /** Google Cloud Storage client configuration */
  options: StorageOptions
}

// Google Cloud Storage options (from @google-cloud/storage)
interface StorageOptions {
  projectId?: string
  keyFilename?: string
  credentials?: {
    client_email: string
    private_key: string
  }
  apiEndpoint?: string
  // ... other GCS options
}
```

## Usage Guides

### Basic File Upload Setup

Step-by-step guide for setting up basic file uploads:

```typescript
// 1. Define your media collection
const Media = {
  slug: 'media',
  upload: {
    staticDir: 'media', // Not used with GCS, but required for type checking
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
    gcsStorage({
      collections: {
        media: true,
      },
      bucket: process.env.GCS_BUCKET,
      options: {
        projectId: process.env.GCS_PROJECT_ID,
        keyFilename: process.env.GCS_KEY_FILE,
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
    gcsStorage({
      collections: {
        // Images: public access, organized by date
        images: {
          prefix: `images/${new Date().getFullYear()}/${new Date().getMonth() + 1}`,
        },
        
        // Documents: private storage
        documents: {
          prefix: 'documents/private',
        },
        
        // Videos: client uploads for large files
        videos: {
          prefix: 'videos',
        },
      },
      bucket: process.env.GCS_BUCKET,
      acl: 'Public', // Make files publicly accessible
      clientUploads: {
        access: ({ collectionSlug, req }) => {
          // Allow client uploads only for videos and authenticated users
          return collectionSlug === 'videos' && Boolean(req.user)
        },
      },
      options: {
        projectId: process.env.GCS_PROJECT_ID,
        credentials: {
          client_email: process.env.GCS_CLIENT_EMAIL,
          private_key: process.env.GCS_PRIVATE_KEY.replace(/\\n/g, '\n'),
        },
      },
    }),
  ],
})
```

### Advanced Patterns

#### Service Account Authentication (Production)

```typescript
gcsStorage({
  collections: { media: true },
  bucket: 'production-files',
  options: {
    projectId: 'my-production-project',
    credentials: {
      client_email: process.env.GCS_CLIENT_EMAIL,
      private_key: process.env.GCS_PRIVATE_KEY.replace(/\\n/g, '\n'),
    },
  },
})
```

#### Development with Emulator

```typescript
gcsStorage({
  collections: { media: true },
  bucket: 'dev-bucket',
  options: {
    projectId: 'test-project',
    apiEndpoint: 'http://localhost:4443', // GCS emulator
    credentials: {
      client_email: 'test@example.com',
      private_key: 'dummy-key',
    },
  },
})
```

#### Dynamic File Organization

```typescript
gcsStorage({
  collections: {
    media: {
      prefix: ({ req }) => {
        const userId = req.user?.id || 'anonymous'
        const date = new Date().toISOString().split('T')[0]
        return `uploads/${userId}/${date}`
      },
    },
  },
  bucket: process.env.GCS_BUCKET,
  options: { /* ... */ },
})
```

## API Reference

### Functions

#### `gcsStorage(options: GcsStorageOptions): Plugin`

Main plugin function that creates the GCS storage adapter.

**Parameters:**
| Parameter | Type | Description |
|-----------|------|-------------|
| options | `GcsStorageOptions` | Configuration object for GCS storage |

**Returns:** `Plugin` - PayloadCMS plugin instance

**Example:**
```typescript
const gcsPlugin = gcsStorage({
  collections: { media: true },
  bucket: 'my-bucket',
  options: { projectId: 'my-project' },
})
```

#### `getGenerateURL({ bucket, getStorageClient }): GenerateURL`

Generates public URLs for stored files using GCS public URL format.

**Parameters:**
| Parameter | Type | Description |
|-----------|------|-------------|
| bucket | `string` | GCS bucket name |
| getStorageClient | `() => Storage` | Function to get GCS client |

**Returns:** Function that generates URLs from filename and prefix

**Example:**
```typescript
const generateURL = getGenerateURL({
  bucket: 'my-bucket',
  getStorageClient: () => storage
})
const url = generateURL({ filename: 'image.jpg', prefix: 'uploads' })
// Returns: "https://storage.googleapis.com/my-bucket/uploads/image.jpg"
```

#### `getHandleUpload(args): HandleUpload`

Creates upload handler for file processing and storage to GCS.

**Parameters:**
| Parameter | Type | Description |
|-----------|------|-------------|
| acl | `'Private' \| 'Public'` | Access control setting |
| bucket | `string` | GCS bucket name |
| getStorageClient | `() => Storage` | Function to get GCS client |
| prefix | `string` | File prefix/path |

**Returns:** Upload handler function

**Example:**
```typescript
const handleUpload = getHandleUpload({
  bucket: 'my-bucket',
  getStorageClient: () => gcsClient,
  prefix: 'uploads/',
  acl: 'Public'
})
```

#### `getHandleDelete(args): HandleDelete`

Creates delete handler for removing files from GCS.

**Parameters:**
| Parameter | Type | Description |
|-----------|------|-------------|
| bucket | `string` | GCS bucket name |
| getStorageClient | `() => Storage` | Function to get GCS client |

**Returns:** Delete handler function

**Example:**
```typescript
const handleDelete = getHandleDelete({
  bucket: 'my-bucket',
  getStorageClient: () => gcsClient,
})
```

### React Components

#### `GcsClientUploadHandler`

Client-side upload handler component for browser-based file uploads to GCS.

**Usage:**
This component is automatically configured when `clientUploads` is enabled. It handles:
- Generating signed URLs for upload
- Performing direct browser-to-GCS uploads
- Error handling and progress tracking

**Example:**
```typescript
// Automatically used when clientUploads is enabled
clientUploads: true
// The GcsClientUploadHandler is imported from '@payloadcms/storage-gcs/client'
```

### TypeScript Types

```typescript
// Main configuration interface
export interface GcsStorageOptions {
  acl?: 'Private' | 'Public'
  bucket: string
  clientUploads?: ClientUploadsConfig
  collections: Partial<Record<UploadCollectionSlug, Omit<CollectionOptions, 'adapter'> | true>>
  enabled?: boolean
  options: StorageOptions
}

// Upload handler interface
export interface HandleUpload {
  (args: {
    data: Record<string, any>
    file: {
      buffer: Buffer
      filename: string
      mimeType: string
    }
  }): Promise<Record<string, any>>
}

// Delete handler interface
export interface HandleDelete {
  (args: {
    doc: { prefix?: string }
    filename: string
  }): Promise<void>
}

// URL generation interface
export interface GenerateURL {
  (args: {
    filename: string
    prefix?: string
  }): string
}

// Static handler interface
export interface StaticHandler {
  (req: PayloadRequest, args: {
    headers: Headers
    params: {
      filename: string
      clientUploadContext?: string
    }
  }): Promise<Response>
}
```

## Integrations

### PayloadCMS Hooks
The package automatically integrates with PayloadCMS lifecycle hooks:

- **Upload hooks**: Processes files during upload operations with automatic metadata handling
- **Delete hooks**: Removes files from GCS when documents are deleted with `ignoreNotFound: true`
- **Access control**: Respects PayloadCMS access control patterns for file access
- **Validation hooks**: Validates file types and sizes according to collection configuration

### Database
The package doesn't require additional database schema changes. It stores:

- **File metadata** in existing PayloadCMS upload fields
- **GCS URLs** are generated dynamically using public URL format
- **Prefix information** for file organization and access control
- **ETags** for caching and conditional requests

### External Services

#### Google Cloud Storage
- **Primary integration** with full Google Cloud Storage API support
- **IAM permissions** required: `storage.objects.create`, `storage.objects.delete`, `storage.objects.get`
- **Service account** authentication for production environments
- **Bucket CORS** configuration for client uploads

#### Google Cloud Platform Services
- **Cloud IAM**: For service account and permission management
- **Cloud Logging**: Automatic integration with GCP logging services
- **Cloud Monitoring**: Built-in metrics and monitoring support

## Troubleshooting

### Common Issues

#### Authentication Failures

**Problem:** "Unable to detect a Project Id in the current environment" or authentication errors

**Solution:**
Ensure proper service account configuration:

```typescript
// For production (using environment variables)
options: {
  projectId: process.env.GCS_PROJECT_ID,
  credentials: {
    client_email: process.env.GCS_CLIENT_EMAIL,
    private_key: process.env.GCS_PRIVATE_KEY.replace(/\\n/g, '\n'),
  },
}

// For development (using key file)
options: {
  projectId: 'my-project',
  keyFilename: './path/to/service-account-key.json',
}
```

**Example:**
```bash
# Verify your service account has proper permissions
gcloud iam service-accounts describe your-service-account@project.iam.gserviceaccount.com
```

#### Client Upload CORS Errors

**Problem:** Client uploads fail with CORS policy errors

**Solution:**
Configure your GCS bucket's CORS policy:

```json
[
  {
    "origin": ["https://yourdomain.com"],
    "method": ["GET", "PUT", "POST"],
    "responseHeader": ["Content-Type", "x-goog-resumable"],
    "maxAgeSeconds": 3600
  }
]
```

**Example:**
```bash
# Using gsutil to set CORS policy
gsutil cors set cors.json gs://your-bucket-name
```

#### File Not Found Errors

**Problem:** Files return 404 errors when accessed

**Solution:**
Verify bucket permissions and file ACLs:

```typescript
// Ensure files are made public if needed
gcsStorage({
  // ...
  acl: 'Public', // Makes uploaded files publicly readable
})
```

#### Large File Upload Failures

**Problem:** Large file uploads timeout or fail

**Solution:**
Enable client uploads for large files:

```typescript
gcsStorage({
  // ...
  clientUploads: true, // Bypass server upload limits
})
```

#### Signed URL Generation Errors

**Problem:** Client uploads fail to generate signed URLs

**Solution:**
Verify service account has `storage.objects.create` permission and proper configuration:

```typescript
// Check your service account permissions
options: {
  projectId: process.env.GCS_PROJECT_ID,
  credentials: {
    client_email: process.env.GCS_CLIENT_EMAIL,
    private_key: process.env.GCS_PRIVATE_KEY.replace(/\\n/g, '\n'),
  },
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

Test GCS connection:
```typescript
// Test GCS connection
import { Storage } from '@google-cloud/storage'

const storage = new Storage({
  projectId: process.env.GCS_PROJECT_ID,
  keyFilename: process.env.GCS_KEY_FILE,
})

// Test bucket access
try {
  const [exists] = await storage.bucket(process.env.GCS_BUCKET).exists()
  console.log('GCS connection successful:', exists)
} catch (error) {
  console.error('GCS connection failed:', error)
}
```

## Performance

### Performance Optimization

**Streaming Uploads**: The package uses Google Cloud Storage's native streaming for efficient memory usage:
```typescript
// Automatically handled - no configuration needed
const gcsFile = storage.bucket(bucket).file(filename)
await gcsFile.save(fileBuffer) // Streams automatically
```

**Client-Side Uploads**: Enable for improved performance and reduced server load:
```typescript
clientUploads: true // Recommended for production
```

**Parallel Processing**: GCS handles concurrent operations efficiently:
```typescript
// Multiple file operations run concurrently
const operations = files.map(file => 
  storage.bucket(bucket).file(file.name).save(file.buffer)
)
await Promise.all(operations)
```

**Caching Headers**: Automatic ETag and caching header management for optimal client-side caching.

**Regional Bucket Placement**: Use regional buckets close to your users:
```bash
# Create bucket in specific region for better performance
gsutil mb -l us-central1 gs://your-bucket-name
```

## Security

**Service Account Security**: Use minimal required permissions:

```json
{
  "bindings": [
    {
      "role": "roles/storage.objectAdmin",
      "members": ["serviceAccount:your-sa@project.iam.gserviceaccount.com"]
    }
  ]
}
```

**Credential Management**: Never commit service account keys to version control:

```bash
# Use environment variables
export GCS_CLIENT_EMAIL="service-account@project.iam.gserviceaccount.com"
export GCS_PRIVATE_KEY="$(cat key.json | jq -r '.private_key')"
```

**Bucket Security**: Configure proper bucket-level security:
```bash
# Remove public access
gsutil iam ch -d allUsers:objectViewer gs://your-bucket

# Add specific permissions
gsutil iam ch user:admin@example.com:objectAdmin gs://your-bucket
```

**Signed URL Expiration**: Keep signed URLs short-lived:
```typescript
// Signed URLs expire after 5 hours (configured in generateSignedURL.ts)
expires: Date.now() + 60 * 60 * 5 // 5 hours
```

**CORS Configuration**: Restrict CORS to specific domains:
```json
{
  "origin": ["https://yourdomain.com", "https://admin.yourdomain.com"],
  "method": ["GET", "PUT"],
  "maxAgeSeconds": 3600
}
```

## Migration

### From @payloadcms/plugin-cloud-storage (Payload 2.x)

The new GCS storage plugin simplifies configuration significantly:

**Before (Payload 2.x):**
```typescript
plugins: [
  cloudStorage({
    collections: {
      media: {
        adapter: gcsAdapter({
          options: { /* ... */ },
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
  gcsStorage({
    collections: {
      media: true,
    },
    bucket: 'my-bucket',
    options: { /* ... */ },
  }),
]
```

**Breaking Changes:**
- Remove `@payloadcms/plugin-cloud-storage` dependency
- Update plugin configuration syntax
- Collections automatically get `disableLocalStorage: true`
- Client uploads configuration syntax changed
- Service account configuration may need updating

## Contributing

Found a bug or have a suggestion? [Open an issue](https://github.com/payloadcms/payload/issues) or submit a Pull Request.

### Development Setup
```bash
# Clone the repository
git clone https://github.com/payloadcms/payload.git
cd payload/packages/storage-gcs

# Install dependencies
pnpm install

# Build the package
pnpm build

# Run tests (if available)
pnpm test
```

### Local Development with GCS Emulator
```bash
# Install and start GCS emulator
gcloud components install cloud-storage-emulator
gcloud beta emulators storage start --host-port=localhost:4443

# Configure your plugin to use emulator
options: {
  apiEndpoint: 'http://localhost:4443',
  projectId: 'test-project',
}
```

## License

This package is licensed under the MIT License. See the [LICENSE.md](LICENSE.md) file for details.

Copyright (c) 2024 Payload. All rights reserved.