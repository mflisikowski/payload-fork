---
title: Azure Blob Storage for Payload
label: Storage Azure
order: 12
desc: Comprehensive Azure Blob Storage adapter for PayloadCMS with client uploads, SAS tokens, and seamless integration.
keywords: [azure, blob-storage, storage, upload, files, cloud, sas-tokens, client-uploads, container]
---

<Banner type="warning">
**Original Documentation**: The content below comes from the official README.md of this package.
Further in the document, you'll find an extended, more detailed version of this documentation.
</Banner>

# Azure Blob Storage for Payload

This package provides a simple way to use [Azure Blob Storage](https://azure.microsoft.com/en-us/products/storage/blobs) with Payload.

**NOTE:** This package removes the need to use `@payloadcms/plugin-cloud-storage` as was needed in Payload 2.x.

## Installation

```sh
pnpm add @payloadcms/storage-azure
```

## Usage

- Configure the `collections` object to specify which collections should use the Azure Blob Storage adapter. The slug _must_ match one of your existing collection slugs.
- When enabled, this package will automatically set `disableLocalStorage` to `true` for each collection.
- When deploying to Vercel, server uploads are limited with 4.5MB. Set `clientUploads` to `true` to do uploads directly on the client. You must allow CORS PUT method to your website.

```ts
import { azureStorage } from '@payloadcms/storage-azure'
import { Media } from './collections/Media'
import { MediaWithPrefix } from './collections/MediaWithPrefix'

export default buildConfig({
  collections: [Media, MediaWithPrefix],
  plugins: [
    azureStorage({
      collections: {
        media: true,
        'media-with-prefix': {
          prefix,
        },
      },
      allowContainerCreate: process.env.AZURE_STORAGE_ALLOW_CONTAINER_CREATE === 'true',
      baseURL: process.env.AZURE_STORAGE_ACCOUNT_BASEURL,
      connectionString: process.env.AZURE_STORAGE_CONNECTION_STRING,
      containerName: process.env.AZURE_STORAGE_CONTAINER_NAME,
    }),
  ],
})
```

### Configuration Options

| Option                 | Description                                                              | Default |
| ---------------------- | ------------------------------------------------------------------------ | ------- |
| `enabled`              | Whether or not to enable the plugin                                      | `true`  |
| `collections`          | Collections to apply the Azure Blob adapter to                           |         |
| `allowContainerCreate` | Whether or not to allow the container to be created if it does not exist | `false` |
| `baseURL`              | Base URL for the Azure Blob storage account                              |         |
| `connectionString`     | Azure Blob storage connection string                                     |         |
| `containerName`        | Azure Blob storage container name                                        |         |
| `clientUploads`        | Do uploads directly on the client to bypass limits on Vercel.            |         |

---

## 📚 Extended Documentation

<Banner type="success">
**Note**: The documentation below has been automatically generated based on source code analysis and contains more detailed information than the original documentation above.
</Banner>

![NPM Version](https://img.shields.io/npm/v/@payloadcms/storage-azure)
![Bundle Size](https://img.shields.io/bundlephobia/minzip/@payloadcms/storage-azure)

## Detailed Overview

The `@payloadcms/storage-azure` package is a comprehensive storage adapter that enables PayloadCMS to seamlessly integrate with Microsoft Azure Blob Storage. This package modernizes file storage by eliminating the need for the previous `@payloadcms/plugin-cloud-storage` approach used in Payload 2.x and provides efficient, scalable file handling with advanced cloud storage features.

Key capabilities include:
- **Native Azure Blob Storage integration** with full API support and automatic client management
- **Intelligent multipart uploads** for files larger than 50MB with optimized streaming and parallel processing
- **Client-side uploads** using SAS (Shared Access Signature) tokens to bypass server limitations
- **Flexible container management** with optional automatic container creation
- **Range request support** for partial content delivery and streaming media
- **Built-in error handling** for Azure-specific scenarios and proper HTTP status codes

The package is designed for developers building applications that require enterprise-grade file storage, content management systems, and applications with significant media handling requirements. It's particularly well-suited for organizations already using Microsoft Azure cloud services.

<Banner type="info">
The package is open-source. [View source code](https://github.com/payloadcms/payload/tree/main/packages/storage-azure). Need help? [Community Help](https://payloadcms.com/community-help).
</Banner>

## System Requirements

- **PayloadCMS**: ^3.0.0 (workspace dependency)
- **Node.js**: ^18.20.2 || >=20.9.0
- **TypeScript**: Supported with full type definitions
- **Azure SDK**: Uses @azure/storage-blob v12.11.0+ for optimal performance

### Additional Requirements
- **Azure Storage Account**: Valid Azure Storage Account with Blob Storage enabled
- **Connection String**: Azure Storage account connection string or access keys
- **Storage Container**: Pre-created Azure Blob Storage container (or enable auto-creation)
- **CORS Configuration**: Required for client-side uploads (if using `clientUploads`)

## Installation

```bash
# npm
npm install @payloadcms/storage-azure

# yarn
yarn add @payloadcms/storage-azure

# pnpm
pnpm add @payloadcms/storage-azure
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
@azure/storage-blob: ^12.11.0
@azure/abort-controller: ^1.1.0
@payloadcms/plugin-cloud-storage: workspace:*
range-parser: ^1.2.1
```

## Quick Start

Basic configuration for immediate use:

```typescript
import { azureStorage } from '@payloadcms/storage-azure'
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
    azureStorage({
      // Required: specify which collections use Azure
      collections: {
        media: true, // Enable for 'media' collection
      },
      // Required: Azure Storage configuration
      allowContainerCreate: process.env.NODE_ENV === 'development',
      baseURL: process.env.AZURE_STORAGE_ACCOUNT_BASEURL!,
      connectionString: process.env.AZURE_STORAGE_CONNECTION_STRING!,
      containerName: process.env.AZURE_STORAGE_CONTAINER_NAME!,
    }),
  ],
})
```

### Environment Variables
```bash
# Required environment variables
AZURE_STORAGE_CONNECTION_STRING=DefaultEndpointsProtocol=https;AccountName=account;AccountKey=key;EndpointSuffix=core.windows.net
AZURE_STORAGE_ACCOUNT_BASEURL=https://youraccount.blob.core.windows.net
AZURE_STORAGE_CONTAINER_NAME=your-container-name

# Optional: auto-create container
AZURE_STORAGE_ALLOW_CONTAINER_CREATE=true
```

## Detailed Configuration

### Main Options

#### `collections`

- **Type**: `Partial<Record<UploadCollectionSlug, CollectionOptions | true>>`
- **Default value**: None
- **Required**: true

Defines which PayloadCMS upload collections should use the Azure Blob Storage adapter. The key must match an existing collection slug exactly.

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

#### `connectionString`

- **Type**: `string`
- **Default value**: None
- **Required**: true

Azure Storage account connection string containing authentication information.

```typescript
connectionString: "DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=mykey;EndpointSuffix=core.windows.net"
```

#### `containerName`

- **Type**: `string`
- **Default value**: None
- **Required**: true

The Azure Blob Storage container name where files will be stored.

```typescript
containerName: 'my-app-files'
```

#### `baseURL`

- **Type**: `string`
- **Default value**: None
- **Required**: true

Base URL for the Azure Blob storage account, used for generating public URLs.

```typescript
baseURL: 'https://myaccount.blob.core.windows.net'
```

#### `allowContainerCreate`

- **Type**: `boolean`
- **Default value**: false
- **Required**: false

Whether to automatically create the container if it doesn't exist. Useful for development environments.

```typescript
// Allow container creation in development
allowContainerCreate: process.env.NODE_ENV === 'development'
```

#### `clientUploads`

- **Type**: `ClientUploadsConfig | boolean`
- **Default value**: false
- **Required**: false

Enables client-side uploads using SAS tokens to bypass server limitations (especially useful for Vercel's 4.5MB limit).

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

**Note**: Requires CORS configuration on your Azure Storage account to allow PUT requests from your domain.

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
export type AzureStorageOptions = {
  /** Whether to allow container creation if it doesn't exist */
  allowContainerCreate: boolean
  
  /** Base URL for the Azure Blob storage account */
  baseURL: string
  
  /** Enable client-side uploads with optional access control */
  clientUploads?: ClientUploadsConfig
  
  /** Collection-specific configurations */
  collections: Partial<Record<UploadCollectionSlug, Omit<CollectionOptions, 'adapter'> | true>>
  
  /** Azure Blob storage connection string */
  connectionString: string
  
  /** Azure Blob storage container name */
  containerName: string
  
  /** Enable/disable the plugin (default: true) */
  enabled?: boolean
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
    staticDir: 'media', // Not used with Azure, but required for type checking
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
    azureStorage({
      collections: {
        media: true,
      },
      allowContainerCreate: false,
      baseURL: process.env.AZURE_STORAGE_ACCOUNT_BASEURL,
      connectionString: process.env.AZURE_STORAGE_CONNECTION_STRING,
      containerName: process.env.AZURE_STORAGE_CONTAINER_NAME,
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
    azureStorage({
      collections: {
        // Images: organized by date
        images: {
          prefix: `images/${new Date().getFullYear()}/${new Date().getMonth() + 1}`,
        },
        
        // Documents: private storage with prefix
        documents: {
          prefix: 'documents/private',
        },
        
        // Videos: client uploads for large files
        videos: {
          prefix: 'videos',
        },
      },
      allowContainerCreate: process.env.NODE_ENV === 'development',
      baseURL: process.env.AZURE_STORAGE_ACCOUNT_BASEURL,
      connectionString: process.env.AZURE_STORAGE_CONNECTION_STRING,
      containerName: process.env.AZURE_STORAGE_CONTAINER_NAME,
      clientUploads: {
        access: ({ collectionSlug, req }) => {
          // Allow client uploads only for videos and authenticated users
          return collectionSlug === 'videos' && Boolean(req.user)
        },
      },
    }),
  ],
})
```

### Advanced Patterns

#### Production Setup with Connection String

```typescript
azureStorage({
  collections: { media: true },
  allowContainerCreate: false,
  baseURL: 'https://production.blob.core.windows.net',
  connectionString: process.env.AZURE_STORAGE_CONNECTION_STRING,
  containerName: 'production-files',
})
```

#### Development with Container Auto-Creation

```typescript
azureStorage({
  collections: { media: true },
  allowContainerCreate: true, // Auto-create containers in dev
  baseURL: 'https://devaccount.blob.core.windows.net',
  connectionString: process.env.AZURE_STORAGE_CONNECTION_STRING,
  containerName: 'dev-files',
})
```

#### Dynamic File Organization

```typescript
azureStorage({
  collections: {
    media: {
      prefix: ({ req }) => {
        const userId = req.user?.id || 'anonymous'
        const date = new Date().toISOString().split('T')[0]
        return `uploads/${userId}/${date}`
      },
    },
  },
  allowContainerCreate: false,
  baseURL: process.env.AZURE_STORAGE_ACCOUNT_BASEURL,
  connectionString: process.env.AZURE_STORAGE_CONNECTION_STRING,
  containerName: process.env.AZURE_STORAGE_CONTAINER_NAME,
})
```

## API Reference

### Functions

#### `azureStorage(options: AzureStorageOptions): Plugin`

Main plugin function that creates the Azure Blob Storage adapter.

**Parameters:**
| Parameter | Type | Description |
|-----------|------|-------------|
| options | `AzureStorageOptions` | Configuration object for Azure storage |

**Returns:** `Plugin` - PayloadCMS plugin instance

**Example:**
```typescript
const azurePlugin = azureStorage({
  collections: { media: true },
  baseURL: 'https://account.blob.core.windows.net',
  connectionString: 'DefaultEndpointsProtocol=https;...',
  containerName: 'files',
  allowContainerCreate: false,
})
```

#### `getGenerateURL({ baseURL, containerName }): GenerateURL`

Generates public URLs for stored files using Azure Blob Storage URL format.

**Parameters:**
| Parameter | Type | Description |
|-----------|------|-------------|
| baseURL | `string` | Azure storage account base URL |
| containerName | `string` | Container name |

**Returns:** Function that generates URLs from filename and prefix

**Example:**
```typescript
const generateURL = getGenerateURL({
  baseURL: 'https://account.blob.core.windows.net',
  containerName: 'files'
})
const url = generateURL({ filename: 'image.jpg', prefix: 'uploads' })
// Returns: "https://account.blob.core.windows.net/files/uploads/image.jpg"
```

#### `getHandleUpload(args): HandleUpload`

Creates upload handler with intelligent multipart upload for large files (>50MB).

**Parameters:**
| Parameter | Type | Description |
|-----------|------|-------------|
| getStorageClient | `() => ContainerClient` | Function to get Azure container client |
| prefix | `string` | File prefix/path |
| collection | `CollectionConfig` | PayloadCMS collection config |

**Returns:** Upload handler function

**Example:**
```typescript
const handleUpload = getHandleUpload({
  getStorageClient: () => containerClient,
  prefix: 'uploads/',
  collection: mediaCollection,
})
```

#### `getHandleDelete(args): HandleDelete`

Creates delete handler for removing files from Azure Blob Storage.

**Parameters:**
| Parameter | Type | Description |
|-----------|------|-------------|
| getStorageClient | `() => ContainerClient` | Function to get Azure container client |
| collection | `CollectionConfig` | PayloadCMS collection config |

**Returns:** Delete handler function with `deleteIfExists` for safe deletion

**Example:**
```typescript
const handleDelete = getHandleDelete({
  getStorageClient: () => containerClient,
  collection: mediaCollection,
})
```

#### `getStorageClient(options): ContainerClient`

Creates and manages Azure Blob Storage container client with connection pooling.

**Parameters:**
| Parameter | Type | Description |
|-----------|------|-------------|
| connectionString | `string` | Azure storage connection string |
| containerName | `string` | Container name |

**Returns:** `ContainerClient` - Cached Azure container client

**Example:**
```typescript
const client = getStorageClient({
  connectionString: process.env.AZURE_STORAGE_CONNECTION_STRING,
  containerName: 'my-files',
})
```

### React Components

#### `AzureClientUploadHandler`

Client-side upload handler component for browser-based file uploads to Azure Blob Storage.

**Usage:**
This component is automatically configured when `clientUploads` is enabled. It handles:
- Generating SAS (Shared Access Signature) tokens for upload
- Performing direct browser-to-Azure uploads with required headers
- Error handling and progress tracking

**Example:**
```typescript
// Automatically used when clientUploads is enabled
clientUploads: true
// The AzureClientUploadHandler is imported from '@payloadcms/storage-azure/client'
```

**Special Headers:**
The client handler automatically sets the required `x-ms-blob-type: BlockBlob` header for Azure compatibility.

### TypeScript Types

```typescript
// Main configuration interface
export type AzureStorageOptions = {
  allowContainerCreate: boolean
  baseURL: string
  clientUploads?: ClientUploadsConfig
  collections: Partial<Record<UploadCollectionSlug, Omit<CollectionOptions, 'adapter'> | true>>
  connectionString: string
  containerName: string
  enabled?: boolean
}

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

// Range parsing result
interface RangeResult {
  start: number
  end: number | undefined
}
```

## Integrations

### PayloadCMS Hooks
The package automatically integrates with PayloadCMS lifecycle hooks:

- **Upload hooks**: Processes files during upload operations with automatic streaming for large files
- **Delete hooks**: Removes files from Azure with `deleteIfExists` to prevent errors on missing files
- **Access control**: Respects PayloadCMS access control patterns for file access
- **Validation hooks**: Validates file types and sizes according to collection configuration

### Database
The package doesn't require additional database schema changes. It stores:

- **File metadata** in existing PayloadCMS upload fields
- **Azure URLs** are generated dynamically using base URL format
- **Prefix information** for file organization and access control
- **ETags** for caching and conditional requests via Azure's built-in support

### External Services

#### Microsoft Azure Blob Storage
- **Primary integration** with full Azure Blob Storage API support
- **Authentication** via connection strings with shared key access
- **Container management** with optional auto-creation capabilities
- **SAS token generation** for secure client-side uploads

#### Azure Services Integration
- **Azure Active Directory**: For advanced authentication scenarios
- **Azure CDN**: For global content delivery (configure base URL)
- **Azure Monitor**: Built-in logging and monitoring support
- **Azure Storage Analytics**: Automatic metrics and logging

## Troubleshooting

### Common Issues

#### Connection String Authentication Failures

**Problem:** "Unable to authenticate" or connection errors

**Solution:**
Verify your Azure Storage connection string format:

```typescript
// Correct connection string format
connectionString: "DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=mykey;EndpointSuffix=core.windows.net"
```

**Example:**
```bash
# Get connection string from Azure CLI
az storage account show-connection-string --name myaccount --resource-group mygroup --query connectionString --output tsv
```

#### Container Not Found Errors

**Problem:** Container does not exist and files fail to upload

**Solution:**
Enable container auto-creation or create container manually:

```typescript
// Option 1: Enable auto-creation
azureStorage({
  // ...
  allowContainerCreate: true,
})

// Option 2: Create container manually
az storage container create --name my-container --connection-string "..."
```

#### Client Upload CORS Errors

**Problem:** Client uploads fail with CORS policy errors

**Solution:**
Configure your Azure Storage account's CORS policy:

```json
[
  {
    "allowedOrigins": ["https://yourdomain.com"],
    "allowedMethods": ["GET", "PUT", "POST"],
    "allowedHeaders": ["*"],
    "exposedHeaders": ["*"],
    "maxAgeInSeconds": 3600
  }
]
```

**Example:**
```bash
# Using Azure CLI to set CORS
az storage cors add --services b --methods PUT POST GET --origins https://yourdomain.com --allowed-headers "*" --exposed-headers "*" --max-age 3600 --connection-string "..."
```

#### Large File Upload Timeouts

**Problem:** Large files (>50MB) timeout during upload

**Solution:**
The package automatically handles large files with streaming uploads, but you can adjust the timeout:

```typescript
// Large files are handled automatically with:
// - 4MB chunk size
// - 4 concurrent uploads
// - 30-minute timeout
// No additional configuration needed
```

#### SAS Token Generation Errors

**Problem:** Client uploads fail to generate SAS tokens

**Solution:**
Ensure your connection string includes the account key (not just SAS token):

```typescript
// Correct: Full connection string with AccountKey
connectionString: "DefaultEndpointsProtocol=https;AccountName=account;AccountKey=key;EndpointSuffix=core.windows.net"

// Incorrect: SAS token in connection string
connectionString: "https://account.blob.core.windows.net/?sv=2021-06-08&ss=..."
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

Test Azure connection:
```typescript
// Test Azure Blob Storage connection
import { BlobServiceClient } from '@azure/storage-blob'

const blobServiceClient = BlobServiceClient.fromConnectionString(
  process.env.AZURE_STORAGE_CONNECTION_STRING
)

// Test container access
try {
  const containerClient = blobServiceClient.getContainerClient('my-container')
  const exists = await containerClient.exists()
  console.log('Azure connection successful:', exists)
} catch (error) {
  console.error('Azure connection failed:', error)
}
```

## Performance

### Performance Optimization

**Intelligent Multipart Uploads**: Files larger than 50MB automatically use streaming uploads with optimized settings:
```typescript
// Automatically configured - no action needed
// - Chunk size: 4MB
// - Concurrent uploads: 4
// - Timeout: 30 minutes
await blockBlobClient.uploadStream(stream, 4 * 1024 * 1024, 4)
```

**Client-Side Uploads**: Enable for improved performance and reduced server load:
```typescript
clientUploads: true // Recommended for production
```

**Range Request Support**: Automatic support for partial content delivery:
```typescript
// Supports HTTP Range requests for:
// - Video streaming
// - Progressive image loading
// - Resume interrupted downloads
```

**Connection Pooling**: Automatic Azure client pooling for efficient resource usage:
```typescript
// Automatically managed - single client instance reused
// No additional configuration needed
```

**Container Auto-Creation**: Only enable in development to avoid production delays:
```typescript
allowContainerCreate: process.env.NODE_ENV === 'development'
```

## Security

**Connection String Security**: Never commit connection strings to version control:

```bash
# Use environment variables
export AZURE_STORAGE_CONNECTION_STRING="DefaultEndpointsProtocol=https;AccountName=account;AccountKey=key;EndpointSuffix=core.windows.net"
```

**SAS Token Configuration**: Client uploads use short-lived SAS tokens:
```typescript
// SAS tokens expire after 30 minutes (configured in generateSignedURL.ts)
expiresOn: new Date(Date.now() + 30 * 60 * 1000)
```

**Container Access Control**: Configure appropriate container access levels:
```bash
# Private container (recommended)
az storage container create --name files --public-access off --connection-string "..."

# Public blob access (only if needed)
az storage container create --name files --public-access blob --connection-string "..."
```

**CORS Configuration**: Restrict CORS to specific domains:
```json
{
  "allowedOrigins": ["https://yourdomain.com", "https://admin.yourdomain.com"],
  "allowedMethods": ["GET", "PUT"],
  "maxAgeInSeconds": 3600
}
```

**Network Security**: Use HTTPS endpoints only:
```typescript
baseURL: 'https://account.blob.core.windows.net' // Always use HTTPS
```

## Migration

### From @payloadcms/plugin-cloud-storage (Payload 2.x)

The new Azure storage plugin simplifies configuration significantly:

**Before (Payload 2.x):**
```typescript
plugins: [
  cloudStorage({
    collections: {
      media: {
        adapter: azureAdapter({
          connectionString: '...',
          containerName: 'files',
          baseURL: 'https://account.blob.core.windows.net',
        }),
      },
    },
  }),
]
```

**After (Payload 3.x):**
```typescript
plugins: [
  azureStorage({
    collections: {
      media: true,
    },
    connectionString: '...',
    containerName: 'files',
    baseURL: 'https://account.blob.core.windows.net',
    allowContainerCreate: false,
  }),
]
```

**Breaking Changes:**
- Remove `@payloadcms/plugin-cloud-storage` dependency
- Update plugin configuration syntax
- Collections automatically get `disableLocalStorage: true`
- Add `allowContainerCreate` configuration option
- Client uploads configuration syntax changed

## Contributing

Found a bug or have a suggestion? [Open an issue](https://github.com/payloadcms/payload/issues) or submit a Pull Request.

### Development Setup
```bash
# Clone the repository
git clone https://github.com/payloadcms/payload.git
cd payload/packages/storage-azure

# Install dependencies
pnpm install

# Build the package
pnpm build

# Run tests (if available)
pnpm test
```

### Local Development with Azurite
```bash
# Install and start Azurite emulator
npm install -g azurite
azurite --silent --location c:\azurite --debug c:\azurite\debug.log

# Configure your plugin to use emulator
connectionString: "DefaultEndpointsProtocol=http;AccountName=devstoreaccount1;AccountKey=Eby8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==;BlobEndpoint=http://127.0.0.1:10000/devstoreaccount1;"
```

## License

This package is licensed under the MIT License. See the [LICENSE.md](LICENSE.md) file for details.

Copyright (c) 2024 Payload. All rights reserved.