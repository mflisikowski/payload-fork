# PayloadCMS Uploads Module - Extended Documentation

The PayloadCMS uploads module provides comprehensive file upload, processing, and storage capabilities with advanced image manipulation, security features, and flexible configuration options.

## Table of Contents

1. [Overview](#overview)
2. [Architecture](#architecture)
3. [Core Components](#core-components)
4. [Configuration](#configuration)
5. [File Processing Pipeline](#file-processing-pipeline)
6. [Image Processing](#image-processing)
7. [Security Features](#security-features)
8. [API Reference](#api-reference)
9. [Usage Examples](#usage-examples)
10. [Performance Optimization](#performance-optimization)
11. [Troubleshooting](#troubleshooting)
12. [Migration Guide](#migration-guide)

## Overview

The uploads module is a core component of PayloadCMS that handles all file upload operations, including:

- **File Upload Processing**: Multipart form data handling with custom parsing
- **Image Manipulation**: Resizing, cropping, format conversion using Sharp
- **Security Protection**: SSRF prevention, file type validation, malicious content filtering
- **Storage Management**: Local file system storage with configurable directories
- **Metadata Handling**: EXIF data processing, focal point positioning
- **Performance Features**: Bulk uploads, image optimization, lazy loading support

### Key Features

- **Advanced Image Processing**: Comprehensive image manipulation with Sharp integration
- **Security First**: Built-in SSRF protection and malicious file detection
- **Flexible Configuration**: Extensive customization options for upload behavior
- **External File Support**: Safe fetching from remote URLs with allowlist controls
- **Admin Integration**: Rich admin UI with drag-and-drop, cropping, and focal point tools

## Architecture

The uploads module follows a modular architecture with clear separation of concerns:

```
uploads/
├── core/               # Core file processing logic
├── security/           # Security and validation features
├── image/             # Image manipulation and processing
├── storage/           # File storage and retrieval
├── admin/             # Admin UI integration
└── types/             # TypeScript definitions
```

### Core Dependencies

- **Sharp**: High-performance image processing library
- **file-type**: MIME type detection from buffer content
- **ipaddr.js**: IP address validation for SSRF protection
- **undici**: HTTP client with interceptor support for safe fetching

## Core Components

### File Processing Pipeline

The file processing pipeline is orchestrated by `generateFileData.ts:generateFileData()`:

```typescript
// Main file processing function
export const generateFileData = async <T>({
  collection: { config: collectionConfig },
  data,
  operation,
  req,
}: Args<T>): Result<T>
```

**Pipeline Stages:**

1. **Validation**: File type, size, and security checks
2. **Processing**: Image manipulation, resizing, format conversion
3. **Storage**: File system operations and path management
4. **Metadata**: EXIF processing and focal point handling
5. **Sizes**: Generation of multiple image sizes

### Security Layer

Security is implemented through multiple components:

- **SSRF Protection** (`safeFetch.ts`): Prevents server-side request forgery
- **File Restrictions** (`checkFileRestrictions.ts`): Validates file types and content
- **Path Sanitization**: Prevents directory traversal attacks
- **IP Filtering**: Blocks requests to private network ranges

### Image Processing Engine

The image processing system uses Sharp for high-performance operations:

- **Resizing** (`imageResizer.ts`): Multi-size image generation
- **Cropping** (`cropImage.ts`): Custom crop operations with focal points
- **Format Conversion**: WebP, AVIF, and other format support
- **Metadata Handling**: EXIF data preservation and manipulation

## Configuration

### Basic Upload Configuration

```typescript
import type { UploadConfig } from 'payload'

const uploadConfig: UploadConfig = {
  // Storage configuration
  staticDir: './uploads',
  disableLocalStorage: false,
  
  // Image processing
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
      crop: 'center',
    }
  ],
  
  // Security settings
  mimeTypes: ['image/*', 'application/pdf'],
  allowRestrictedFileTypes: false,
  
  // External file handling
  pasteURL: {
    allowList: [
      {
        protocol: 'https',
        hostname: 'cdn.example.com'
      }
    ]
  }
}
```

### Advanced Configuration Options

#### Image Processing Options

```typescript
const advancedImageConfig: UploadConfig = {
  // Sharp constructor options
  constructorOptions: {
    sequentialRead: true,
    limitInputPixels: false
  },
  
  // Format options for output
  formatOptions: {
    format: 'webp',
    options: {
      quality: 80,
      effort: 4
    }
  },
  
  // Resize options for original image
  resizeOptions: {
    width: 2000,
    height: 2000,
    fit: 'inside',
    withoutEnlargement: true
  },
  
  // Trim whitespace
  trimOptions: {
    background: 'white',
    threshold: 10
  },
  
  // Metadata handling
  withMetadata: true,
  
  // Focal point and cropping
  focalPoint: true,
  crop: true
}
```

#### Security Configuration

```typescript
const securityConfig: UploadConfig = {
  // File type restrictions
  mimeTypes: [
    'image/jpeg',
    'image/png', 
    'image/webp',
    'application/pdf'
  ],
  
  // External URL fetching
  pasteURL: {
    allowList: [
      {
        protocol: 'https',
        hostname: 'images.unsplash.com',
        pathname: '/photo-*'
      }
    ]
  },
  
  // Skip SSRF protection for trusted sources
  skipSafeFetch: [
    {
      protocol: 'https',
      hostname: 'trusted-cdn.example.com'
    }
  ],
  
  // Custom header filtering for external requests
  externalFileHeaderFilter: (headers) => {
    // Remove sensitive headers
    delete headers['cookie']
    delete headers['authorization']
    return headers
  }
}
```

## File Processing Pipeline

### 1. File Reception and Validation

The pipeline begins when a file is received through the admin UI or API:

```typescript
// File validation process
await checkFileRestrictions({
  collection: collectionConfig,
  file,
  req,
})
```

**Validation Steps:**
- MIME type verification against allowed types
- File size validation
- Malicious content detection
- Extension validation

### 2. Image Analysis and Metadata Extraction

For image files, the system extracts metadata and analyzes properties:

```typescript
// Get image dimensions
const dimensions = await getImageSize(file)

// Extract EXIF data if present
const metadata = await sharpFile.metadata()
```

### 3. Image Processing and Transformation

The core processing applies configured transformations:

```typescript
// Apply resizing, format conversion, and optimization
if (resizeOptions) {
  sharpFile = sharpFile.resize(resizeOptions)
}
if (formatOptions) {
  sharpFile = sharpFile.toFormat(formatOptions.format, formatOptions.options)
}
```

### 4. Multiple Size Generation

The system generates multiple image sizes based on configuration:

```typescript
const { sizeData, sizesToSave } = await resizeAndTransformImageSizes({
  config: collectionConfig,
  dimensions,
  file,
  imageSizes,
  // ... other options
})
```

### 5. File Storage

Finally, files are saved to the configured storage location:

```typescript
const filesToSave: FileToSave[] = [
  {
    buffer: processedFileBuffer,
    path: `${staticPath}/${filename}`
  }
]
```

## Image Processing

### Supported Image Formats

The uploads module supports a wide range of image formats through Sharp:

- **Input Formats**: JPEG, PNG, WebP, AVIF, TIFF, SVG, GIF
- **Output Formats**: JPEG, PNG, WebP, AVIF, TIFF
- **Animated Formats**: GIF, WebP with animation support

### Image Resizing

#### Basic Resizing

```typescript
const imageSize: ImageSize = {
  name: 'medium',
  width: 800,
  height: 600,
  fit: 'cover', // 'cover', 'contain', 'fill', 'inside', 'outside'
  position: 'center' // 'center', 'top', 'bottom', 'left', 'right'
}
```

#### Advanced Resizing Options

```typescript
const advancedImageSize: ImageSize = {
  name: 'hero',
  width: 1200,
  height: 600,
  fit: 'cover',
  position: 'entropy', // Use entropy-based positioning
  withoutEnlargement: true, // Don't upscale small images
  
  // Custom format for this size
  formatOptions: {
    format: 'webp',
    options: { quality: 85 }
  },
  
  // Custom filename generation
  generateImageName: ({ originalName, width, height, extension }) => {
    return `${originalName}-hero-${width}x${height}.${extension}`
  }
}
```

### Image Cropping

The module supports both automatic and manual cropping:

#### Automatic Cropping

```typescript
// Crop using Smart Crop (entropy-based)
const smartCropSize: ImageSize = {
  name: 'smart-crop',
  width: 400,
  height: 400,
  fit: 'cover',
  position: 'entropy'
}

// Crop using attention-based positioning
const attentionCropSize: ImageSize = {
  name: 'attention-crop',
  width: 400,
  height: 400,
  fit: 'cover',
  position: 'attention'
}
```

#### Manual Cropping with Focal Points

```typescript
// Enable focal point selection in admin
const focalPointConfig: UploadConfig = {
  focalPoint: true,
  crop: true,
  imageSizes: [
    {
      name: 'cropped',
      width: 600,
      height: 400,
      fit: 'cover'
      // Focal point will be used for positioning
    }
  ]
}
```

### Format Conversion and Optimization

#### Global Format Conversion

```typescript
const optimizedConfig: UploadConfig = {
  // Convert all images to WebP
  formatOptions: {
    format: 'webp',
    options: {
      quality: 80,
      effort: 4 // Higher effort = better compression
    }
  }
}
```

#### Per-Size Format Conversion

```typescript
const mixedFormatConfig: UploadConfig = {
  imageSizes: [
    {
      name: 'thumbnail',
      width: 200,
      height: 200,
      formatOptions: {
        format: 'webp',
        options: { quality: 70 }
      }
    },
    {
      name: 'full',
      width: 2000,
      height: 2000,
      formatOptions: {
        format: 'jpeg',
        options: { quality: 90 }
      }
    }
  ]
}
```

## Security Features

### SSRF Protection

The module includes comprehensive Server-Side Request Forgery (SSRF) protection:

```typescript
// Safe external file fetching with IP validation
export const safeFetch = async (...args: Parameters<typeof undiciFetch>) => {
  const [unverifiedUrl, options] = args
  
  // Validate URL and resolve hostname
  const url = new URL(unverifiedUrl)
  
  // Check if IP address is safe (not private/localhost)
  if (ipaddr.isValid(hostname)) {
    if (!isSafeIp(hostname)) {
      throw new Error(`Blocked unsafe attempt to ${hostname}`)
    }
  }
  
  // Use custom dispatcher with lookup interceptor
  return await undiciFetch(url, {
    ...options,
    dispatcher: safeDispatcher,
  })
}
```

### File Type Validation

Multiple layers of file type validation ensure security:

```typescript
// MIME type validation
const checkFileRestrictions = async ({ 
  collection, 
  file, 
  req 
}: checkFileRestrictionsParams) => {
  const { mimeTypes, allowRestrictedFileTypes } = collection.upload
  
  // Check against allowed MIME types
  if (mimeTypes && !mimeTypes.includes(file.mimetype)) {
    throw new ValidationError('Invalid file type')
  }
  
  // Check against dangerous file types
  if (!allowRestrictedFileTypes && isDangerousFileType(file)) {
    throw new ValidationError('Restricted file type')
  }
}
```

### Path Sanitization

File paths are sanitized to prevent directory traversal attacks:

```typescript
// Sanitize filename to prevent directory traversal
const baseFilename = sanitize(file.name.substring(0, file.name.lastIndexOf('.')) || file.name)

// Validate incoming file paths
if (filename && (filename.includes('../') || filename.includes('..\\'))) {
  throw new Forbidden(req.t)
}
```

## API Reference

### Core Functions

#### `generateFileData<T>(args: Args<T>): Promise<Result<T>>`

Main file processing function that handles the complete upload pipeline.

**Parameters:**
- `collection`: Collection configuration with upload settings
- `data`: Incoming form data
- `operation`: 'create' | 'update'
- `req`: Payload request object with file data
- `overwriteExistingFiles?`: Whether to overwrite existing files
- `throwOnMissingFile?`: Whether to throw error if no file provided

**Returns:**
- `data`: Updated document data with file information
- `files`: Array of files to save to storage

#### `resizeAndTransformImageSizes(args: ResizeArgs): Promise<ImageSizesResult>`

Generates multiple image sizes based on configuration.

**Parameters:**
- `config`: Collection configuration
- `dimensions`: Original image dimensions
- `file`: File data
- `req`: Request object
- `sharp`: Sharp instance
- `staticPath`: Storage directory path

**Returns:**
- `sizeData`: Object containing size metadata
- `sizesToSave`: Array of processed image files
- `focalPoint`: Focal point coordinates if enabled

#### `safeFetch(...args: Parameters<typeof undiciFetch>): Promise<Response>`

SSRF-protected fetch function for external resources.

**Parameters:**
- Standard fetch API parameters

**Returns:**
- Response object from successful fetch

**Throws:**
- Error for blocked/unsafe requests

### Type Definitions

#### `UploadConfig`

```typescript
export type UploadConfig = {
  // Storage
  staticDir?: string
  disableLocalStorage?: boolean
  
  // File processing
  imageSizes?: ImageSize[]
  formatOptions?: ImageUploadFormatOptions
  resizeOptions?: ResizeOptions
  constructorOptions?: SharpOptions
  trimOptions?: ImageUploadTrimOptions
  
  // Security
  mimeTypes?: string[]
  allowRestrictedFileTypes?: boolean
  pasteURL?: { allowList: AllowList } | false
  skipSafeFetch?: AllowList | boolean
  externalFileHeaderFilter?: (headers: Record<string, string>) => Record<string, string>
  
  // Features
  focalPoint?: boolean
  crop?: boolean
  bulkUpload?: boolean
  displayPreview?: boolean
  withMetadata?: WithMetadata
  
  // Admin
  adminThumbnail?: GetAdminThumbnail | string
  filesRequiredOnCreate?: boolean
  hideFileInputOnCreate?: boolean
  hideRemoveFile?: boolean
  cacheTags?: boolean
  
  // Advanced
  handlers?: Array<(req: PayloadRequest, args: any) => Promise<Response> | Response | void>
  modifyResponseHeaders?: ({ headers }: { headers: Headers }) => Headers | void
  filenameCompoundIndex?: string[]
}
```

#### `ImageSize`

```typescript
export type ImageSize = {
  name: string
  width?: number
  height?: number
  fit?: 'cover' | 'contain' | 'fill' | 'inside' | 'outside'
  position?: string | number
  withoutEnlargement?: boolean
  formatOptions?: ImageUploadFormatOptions
  trimOptions?: ImageUploadTrimOptions
  generateImageName?: GenerateImageName
} & Omit<ResizeOptions, 'withoutEnlargement'>
```

#### `FileData`

```typescript
export type FileData = {
  filename: string
  filesize: number
  width: number
  height: number
  mimeType: string
  focalX?: number
  focalY?: number
  sizes: FileSizes
  url?: string
  tempFilePath?: string
}
```

## Usage Examples

### Basic File Upload Collection

```typescript
import type { CollectionConfig } from 'payload'

const Media: CollectionConfig = {
  slug: 'media',
  upload: {
    staticDir: './uploads/media',
    mimeTypes: ['image/*', 'application/pdf'],
    imageSizes: [
      {
        name: 'thumbnail',
        width: 300,
        height: 300,
        position: 'centre'
      },
      {
        name: 'card',
        width: 768,
        height: 432,
        position: 'centre'
      }
    ]
  },
  fields: [
    {
      name: 'alt',
      type: 'text',
      required: true
    }
  ]
}
```

### Advanced Image Processing

```typescript
const Photos: CollectionConfig = {
  slug: 'photos',
  upload: {
    staticDir: './uploads/photos',
    
    // Enable advanced features
    focalPoint: true,
    crop: true,
    
    // Optimize for web delivery
    formatOptions: {
      format: 'webp',
      options: {
        quality: 85,
        effort: 4
      }
    },
    
    // Multiple optimized sizes
    imageSizes: [
      {
        name: 'thumbnail',
        width: 200,
        height: 200,
        fit: 'cover',
        formatOptions: {
          format: 'webp',
          options: { quality: 70 }
        }
      },
      {
        name: 'medium',
        width: 800,
        height: 600,
        fit: 'inside',
        withoutEnlargement: true
      },
      {
        name: 'large',
        width: 1600,
        height: 1200,
        fit: 'inside',
        withoutEnlargement: true,
        formatOptions: {
          format: 'jpeg',
          options: { quality: 90 }
        }
      }
    ],
    
    // Custom resize for originals
    resizeOptions: {
      width: 2400,
      height: 2400,
      fit: 'inside',
      withoutEnlargement: true
    }
  },
  fields: [
    {
      name: 'title',
      type: 'text',
      required: true
    },
    {
      name: 'description',
      type: 'textarea'
    }
  ]
}
```

### External URL Fetching

```typescript
const ExternalImages: CollectionConfig = {
  slug: 'external-images',
  upload: {
    staticDir: './uploads/external',
    
    // Allow fetching from specific domains
    pasteURL: {
      allowList: [
        {
          protocol: 'https',
          hostname: 'images.unsplash.com'
        },
        {
          protocol: 'https',
          hostname: 'cdn.pixabay.com',
          pathname: '/photo/*'
        }
      ]
    },
    
    // Custom header filtering
    externalFileHeaderFilter: (headers) => {
      // Add custom headers for external requests
      headers['User-Agent'] = 'PayloadCMS/1.0'
      
      // Remove sensitive headers
      delete headers['cookie']
      delete headers['authorization']
      
      return headers
    }
  },
  fields: [
    {
      name: 'source',
      type: 'text',
      label: 'Image Source URL'
    }
  ]
}
```

### Custom Upload Handlers

```typescript
const CustomHandlers: CollectionConfig = {
  slug: 'custom-uploads',
  upload: {
    staticDir: './uploads/custom',
    
    // Custom handlers for file serving
    handlers: [
      // Watermark handler
      async (req, { doc, params }) => {
        if (params.filename.includes('-watermarked')) {
          // Apply watermark and return custom response
          const watermarkedBuffer = await applyWatermark(doc)
          return new Response(watermarkedBuffer, {
            headers: {
              'Content-Type': doc.mimeType,
              'Content-Length': watermarkedBuffer.length.toString()
            }
          })
        }
        // Continue to next handler
        return null
      },
      
      // Analytics handler
      async (req, { doc, params }) => {
        // Log download analytics
        await logDownload({
          fileId: doc.id,
          userAgent: req.headers.get('user-agent'),
          ip: req.ip
        })
        // Continue to default handler
        return null
      }
    ],
    
    // Custom response headers
    modifyResponseHeaders: ({ headers }) => {
      headers.set('Cache-Control', 'public, max-age=31536000')
      headers.set('X-Custom-Header', 'PayloadCMS')
      return headers
    }
  }
}
```

## Performance Optimization

### Image Optimization Strategies

#### 1. Format Selection

Choose appropriate formats based on use case:

```typescript
const optimizedFormats: UploadConfig = {
  imageSizes: [
    // WebP for modern browsers with fallback
    {
      name: 'modern',
      width: 800,
      height: 600,
      formatOptions: {
        format: 'webp',
        options: { quality: 80, effort: 4 }
      }
    },
    // JPEG fallback for older browsers
    {
      name: 'fallback',
      width: 800,
      height: 600,
      formatOptions: {
        format: 'jpeg',
        options: { quality: 85, progressive: true }
      }
    }
  ]
}
```

#### 2. Progressive Loading

Configure sizes for progressive loading:

```typescript
const progressiveConfig: UploadConfig = {
  imageSizes: [
    // Tiny placeholder for instant loading
    {
      name: 'placeholder',
      width: 20,
      height: 20,
      formatOptions: {
        format: 'jpeg',
        options: { quality: 50 }
      }
    },
    // Low quality for fast loading
    {
      name: 'lqip',
      width: 200,
      height: 150,
      formatOptions: {
        format: 'webp',
        options: { quality: 30 }
      }
    },
    // Full quality for final display
    {
      name: 'full',
      width: 1200,
      height: 900,
      formatOptions: {
        format: 'webp',
        options: { quality: 85 }
      }
    }
  ]
}
```

#### 3. Smart Compression

Use adaptive quality based on image content:

```typescript
const smartCompression: UploadConfig = {
  imageSizes: [
    {
      name: 'adaptive',
      width: 1000,
      height: 750,
      formatOptions: {
        format: 'webp',
        options: {
          quality: 85,
          effort: 6, // Higher effort for better compression
          smartSubsample: true
        }
      }
    }
  ],
  
  // Global optimization for originals
  resizeOptions: {
    width: 2400,
    height: 1800,
    fit: 'inside',
    withoutEnlargement: true
  },
  
  // Optimize Sharp performance
  constructorOptions: {
    sequentialRead: true,
    limitInputPixels: false
  }
}
```

### Storage Optimization

#### 1. Directory Structure

Organize files efficiently:

```typescript
const optimizedStorage: UploadConfig = {
  staticDir: './uploads',
  
  // Custom filename generation for better organization
  imageSizes: [
    {
      name: 'optimized',
      width: 800,
      height: 600,
      generateImageName: ({ originalName, width, height, extension }) => {
        const date = new Date().toISOString().slice(0, 7) // YYYY-MM
        return `${date}/${originalName}-${width}x${height}.${extension}`
      }
    }
  ]
}
```

#### 2. Bulk Upload Optimization

Configure for efficient bulk operations:

```typescript
const bulkOptimized: UploadConfig = {
  bulkUpload: true,
  
  // Reduce processing overhead for bulk uploads
  constructorOptions: {
    sequentialRead: false, // Parallel processing
    limitInputPixels: 268402689 // ~16MP limit
  },
  
  // Efficient thumbnail generation
  imageSizes: [
    {
      name: 'bulk-thumb',
      width: 200,
      height: 200,
      formatOptions: {
        format: 'webp',
        options: { quality: 60, effort: 1 } // Fast processing
      }
    }
  ]
}
```

### Memory Management

#### 1. Sharp Configuration

Optimize Sharp for your environment:

```typescript
const memoryOptimized: UploadConfig = {
  constructorOptions: {
    // Reduce memory usage for large images
    sequentialRead: true,
    limitInputPixels: 134217728, // ~8MP limit
    
    // Enable disk caching for large operations
    failOnError: false,
    
    // Optimize for specific image types
    density: 72 // DPI for vector images
  }
}
```

#### 2. Processing Limits

Set appropriate limits:

```typescript
const processLimits: UploadConfig = {
  // Limit maximum image sizes
  resizeOptions: {
    width: 4000,
    height: 4000,
    fit: 'inside',
    withoutEnlargement: true,
    
    // Prevent excessive processing
    kernel: 'lanczos3'
  },
  
  // Efficient format conversion
  formatOptions: {
    format: 'webp',
    options: {
      quality: 80,
      effort: 3, // Balance quality/speed
      nearLossless: false
    }
  }
}
```

## Troubleshooting

### Common Issues and Solutions

#### 1. File Upload Failures

**Issue**: Files fail to upload with generic error message

**Debugging Steps:**

```typescript
// Enable detailed error logging
const debugConfig: UploadConfig = {
  // Check file restrictions
  mimeTypes: ['image/*'], // Ensure MIME type is allowed
  allowRestrictedFileTypes: false, // Check if file type is restricted
  
  // Verify storage configuration
  staticDir: './uploads', // Ensure directory exists and is writable
  disableLocalStorage: false, // Check if local storage is enabled
}

// Log file details for debugging
console.log('File details:', {
  name: file.name,
  size: file.size,
  mimetype: file.mimetype
})
```

**Common Solutions:**
- Verify file MIME type is in allowed list
- Check file size limits in server configuration
- Ensure upload directory has write permissions
- Validate file extension matches MIME type

#### 2. Image Processing Errors

**Issue**: Images fail to process or generate sizes

**Debugging Steps:**

```typescript
// Check Sharp availability and configuration
const sharpDebug = {
  version: sharp.versions,
  format: sharp.format,
  // Log Sharp errors
  constructorOptions: {
    failOnError: false, // Continue processing on errors
    sequentialRead: true // Reduce memory usage
  }
}

// Validate image dimensions and format
try {
  const metadata = await sharp(fileBuffer).metadata()
  console.log('Image metadata:', metadata)
} catch (error) {
  console.error('Sharp processing error:', error)
}
```

**Common Solutions:**
- Update Sharp to latest version
- Check if image format is supported
- Reduce image size limits for memory constraints
- Validate constructor options compatibility

#### 3. SSRF and External Fetching Issues

**Issue**: External URLs fail to fetch or are blocked

**Debugging Steps:**

```typescript
// Debug SSRF protection
const debugSafeFetch = async (url: string) => {
  try {
    const response = await safeFetch(url)
    console.log('Fetch successful:', response.status)
  } catch (error) {
    console.error('SSRF error:', error.message)
    
    // Check if URL is in allowlist
    const parsedUrl = new URL(url)
    console.log('URL details:', {
      protocol: parsedUrl.protocol,
      hostname: parsedUrl.hostname,
      pathname: parsedUrl.pathname
    })
  }
}
```

**Common Solutions:**
- Add domains to pasteURL allowlist
- Check if skipSafeFetch is configured correctly
- Verify external URLs are accessible
- Update allowlist patterns to match URL structure

#### 4. Focal Point and Cropping Issues

**Issue**: Focal points not working or cropping produces unexpected results

**Debugging Steps:**

```typescript
// Debug focal point data
const debugFocalPoint = (uploadEdits: UploadEdits, fileData: FileData) => {
  console.log('Upload edits:', uploadEdits)
  console.log('Current focal point:', {
    x: fileData.focalX,
    y: fileData.focalY
  })
  
  // Check if focal point changed
  const shouldReupload = uploadEdits.focalPoint && 
    (uploadEdits.focalPoint.x !== fileData.focalX || 
     uploadEdits.focalPoint.y !== fileData.focalY)
  
  console.log('Should reprocess:', shouldReupload)
}
```

**Common Solutions:**
- Ensure focalPoint is enabled in configuration
- Verify crop dimensions are within image bounds
- Check if focal point coordinates are valid (0-100 range)
- Update admin UI components for focal point selection

### Performance Issues

#### 1. Slow Upload Processing

**Symptoms**: File uploads take excessive time to complete

**Optimization Steps:**

```typescript
// Performance optimization configuration
const performanceConfig: UploadConfig = {
  // Reduce processing overhead
  constructorOptions: {
    sequentialRead: false, // Enable parallel processing
    limitInputPixels: false // Remove pixel limits if sufficient memory
  },
  
  // Optimize image sizes
  imageSizes: [
    {
      name: 'optimized',
      width: 800,
      height: 600,
      formatOptions: {
        format: 'webp',
        options: {
          quality: 80,
          effort: 2 // Reduce compression effort for speed
        }
      }
    }
  ],
  
  // Skip metadata processing if not needed
  withMetadata: false
}
```

#### 2. High Memory Usage

**Symptoms**: Server runs out of memory during image processing

**Memory Optimization:**

```typescript
// Memory-efficient configuration
const memoryConfig: UploadConfig = {
  constructorOptions: {
    sequentialRead: true, // Process images sequentially
    limitInputPixels: 134217728 // Limit to ~8MP images
  },
  
  // Reduce maximum image dimensions
  resizeOptions: {
    width: 2000,
    height: 2000,
    fit: 'inside',
    withoutEnlargement: true
  },
  
  // Use efficient formats
  formatOptions: {
    format: 'webp',
    options: {
      quality: 75,
      effort: 1 // Minimal compression effort
    }
  }
}
```

### Storage Issues

#### 1. Disk Space Management

**Issue**: Upload directory consuming excessive disk space

**Solutions:**

```typescript
// Implement file cleanup strategy
const cleanupConfig: UploadConfig = {
  // Generate fewer, more targeted sizes
  imageSizes: [
    {
      name: 'thumbnail',
      width: 200,
      height: 200,
      formatOptions: {
        format: 'webp',
        options: { quality: 70 }
      }
    },
    {
      name: 'display',
      width: 1200,
      height: 900,
      formatOptions: {
        format: 'webp',
        options: { quality: 85 }
      }
    }
  ],
  
  // Compress original files
  resizeOptions: {
    width: 2400,
    height: 1800,
    fit: 'inside',
    withoutEnlargement: true
  }
}

// Implement periodic cleanup
const cleanupOldFiles = async () => {
  const cutoffDate = new Date()
  cutoffDate.setDays(cutoffDate.getDate() - 30) // 30 days ago
  
  // Clean up orphaned files
  // Implementation depends on your storage strategy
}
```

#### 2. File Path Issues

**Issue**: Files not found or incorrect URLs generated

**Debugging:**

```typescript
// Debug file path generation
const debugFilePath = (staticDir: string, filename: string) => {
  const fullPath = `${staticDir}/${filename}`
  console.log('Generated path:', fullPath)
  
  // Check if file exists
  const exists = fs.existsSync(fullPath)
  console.log('File exists:', exists)
  
  if (!exists) {
    // List directory contents
    const files = fs.readdirSync(staticDir)
    console.log('Directory contents:', files)
  }
}
```

### Error Codes and Messages

Common error codes and their meanings:

| Error Code | Message | Cause | Solution |
|------------|---------|-------|----------|
| `UPLOAD_INVALID_FILE_TYPE` | Invalid file type | MIME type not allowed | Add MIME type to mimeTypes array |
| `UPLOAD_FILE_TOO_LARGE` | File too large | File exceeds size limit | Increase server upload limits |
| `UPLOAD_MISSING_FILE` | No file provided | File not included in request | Ensure file is properly uploaded |
| `SSRF_BLOCKED` | Blocked unsafe request | URL points to private IP | Add domain to allowlist or use public URL |
| `SHARP_PROCESSING_ERROR` | Image processing failed | Sharp cannot process image | Check image format and Sharp installation |
| `STORAGE_PERMISSION_ERROR` | Cannot write file | Insufficient permissions | Grant write access to upload directory |

## Migration Guide

### Upgrading from Previous Versions

#### Version 2.x to 3.x Changes

**Breaking Changes:**
- `FileSize` type deprecated in favor of `FileSizeImproved`
- SSRF protection enabled by default
- Sharp constructor options moved to `constructorOptions`

**Migration Steps:**

```typescript
// Before (v2.x)
const oldConfig: UploadConfig = {
  imageSizes: [
    {
      name: 'thumb',
      width: 300,
      height: 300,
      crop: 'center' // Deprecated
    }
  ]
}

// After (v3.x)
const newConfig: UploadConfig = {
  imageSizes: [
    {
      name: 'thumb',
      width: 300,
      height: 300,
      position: 'center' // Use position instead of crop
    }
  ],
  
  // Add SSRF configuration if using external URLs
  pasteURL: {
    allowList: [
      {
        protocol: 'https',
        hostname: 'trusted-domain.com'
      }
    ]
  }
}
```

#### Custom Storage Adapters

**Before:**
```typescript
// Custom storage was handled through hooks
const customStorageHook = async (args) => {
  // Custom storage logic
}
```

**After:**
```typescript
// Use handlers for custom storage behavior
const customStorageConfig: UploadConfig = {
  handlers: [
    async (req, { doc, params }) => {
      // Custom storage logic
      await customStorageProvider.save(doc)
      
      // Return custom response or null to continue
      return null
    }
  ]
}
```

### Database Schema Updates

When upgrading, you may need to update your database schema:

```sql
-- Add focal point columns if enabling focal point feature
ALTER TABLE media ADD COLUMN focalX DECIMAL(5,2);
ALTER TABLE media ADD COLUMN focalY DECIMAL(5,2);

-- Add filename compound index if configured
CREATE INDEX idx_media_filename_compound ON media (filename, otherField);
```

### Configuration Migration

Use this helper to migrate old configurations:

```typescript
const migrateUploadConfig = (oldConfig: any): UploadConfig => {
  const newConfig: UploadConfig = { ...oldConfig }
  
  // Migrate crop to position
  if (oldConfig.imageSizes) {
    newConfig.imageSizes = oldConfig.imageSizes.map((size: any) => ({
      ...size,
      position: size.crop || size.position || 'center'
    }))
  }
  
  // Add default SSRF protection
  if (!newConfig.pasteURL && !newConfig.skipSafeFetch) {
    newConfig.pasteURL = false // Disable external fetching by default
  }
  
  return newConfig
}
```

---

This comprehensive documentation covers all aspects of the PayloadCMS uploads module. For additional support, consult the [official PayloadCMS documentation](https://payloadcms.com/docs) or reach out to the community forums.