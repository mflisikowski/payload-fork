---
title: Error Handling System
label: errors
order: 50
desc: Comprehensive error handling system for PayloadCMS with custom error classes, validation errors, and API error responses
keywords: [error, handling, validation, api, exceptions, http, status, payload, cms]
---

![NPM Version](https://img.shields.io/npm/v/payload)
![Bundle Size](https://img.shields.io/bundlephobia/minzip/payload)

## Overview

PayloadCMS provides a comprehensive error handling system designed to provide consistent, structured, and meaningful error responses across the entire application. The error system includes custom error classes for different scenarios, internationalization support, and proper HTTP status code mapping.

The error handling system serves as the foundation for:
- **API Error Responses**: Standardized error responses with proper HTTP status codes
- **Validation Errors**: Field-level validation with detailed error messages
- **Authentication & Authorization**: Security-related error handling
- **File Operations**: Upload, download, and file management error handling
- **Configuration Errors**: Development-time configuration validation

<Banner type="info">
The error system is integrated throughout PayloadCMS. [View source code](https://github.com/payloadcms/payload/tree/main/packages/payload/src/errors). Need help? [Community Help](https://payloadcms.com/community-help).
</Banner>

## System Requirements

- **PayloadCMS**: ^3.0.0
- **Node.js**: ^18.20.2 || >=20.9.0
- **TypeScript**: ^5.0.0 (recommended)

## Core Error Classes

### APIError

The base error class that all other PayloadCMS errors extend. It provides structured error handling with HTTP status codes and additional data.

```typescript
import { APIError } from 'payload/errors'

// Basic usage
throw new APIError('Something went wrong', 500)

// With additional data
throw new APIError('Resource not found', 404, { resourceId: '123' })

// With public message (visible to end users)
throw new APIError('Invalid input', 400, { field: 'email' }, true)
```

**Properties:**
- `message: string` - Error message
- `status: number` - HTTP status code (default: 500)
- `data: object | null` - Additional error data
- `isPublic: boolean` - Whether the error message should be visible to users
- `isOperational: boolean` - Always true for PayloadCMS errors

### ValidationError

Handles field-level validation errors with support for multiple fields and internationalization.

```typescript
import { ValidationError } from 'payload/errors'
import type { ValidationFieldError } from 'payload/errors'

const fieldErrors: ValidationFieldError[] = [
  {
    path: 'email',
    message: 'Email is required',
    label: 'Email Address'
  },
  {
    path: 'password',
    message: 'Password must be at least 8 characters',
    label: { en: 'Password', es: 'Contraseña' }
  }
]

throw new ValidationError({
  errors: fieldErrors,
  collection: 'users'
})
```

**ValidationFieldError Interface:**
```typescript
type ValidationFieldError = {
  label?: LabelFunction | StaticLabel
  message: string
  path: string
}
```

## Authentication & Authorization Errors

### AuthenticationError

Used for login failures and authentication issues.

```typescript
import { AuthenticationError } from 'payload/errors'

// Basic authentication error
throw new AuthenticationError()

// With translation support
throw new AuthenticationError(req.t)

// Username-based authentication
throw new AuthenticationError(req.t, true)
```

### Forbidden

Used when users lack permission to perform an action.

```typescript
import { Forbidden } from 'payload/errors'

// Basic forbidden error
throw new Forbidden()

// With translation
throw new Forbidden(req.t)
```

### UnauthorizedError

For cases where authentication is required but not provided.

```typescript
import { UnauthorizedError } from 'payload/errors'

throw new UnauthorizedError(req.t)
```

## File Operation Errors

### FileUploadError

Handles file upload failures.

```typescript
import { FileUploadError } from 'payload/errors'

throw new FileUploadError(req.t)
```

### FileRetrievalError

For file download and retrieval issues.

```typescript
import { FileRetrievalError } from 'payload/errors'

throw new FileRetrievalError(req.t)
```

### MissingFile

When required files are not found.

```typescript
import { MissingFile } from 'payload/errors'

throw new MissingFile(req.t)
```

## Configuration Errors

These errors help developers identify configuration issues during development.

### InvalidConfiguration

```typescript
import { InvalidConfiguration } from 'payload/errors'

throw new InvalidConfiguration('Database connection string is required')
```

### DuplicateCollection

```typescript
import { DuplicateCollection } from 'payload/errors'

throw new DuplicateCollection('users')
```

### InvalidFieldName

```typescript
import { InvalidFieldName } from 'payload/errors'

throw new InvalidFieldName('field-name')
```

### ReservedFieldName

```typescript
import { ReservedFieldName } from 'payload/errors'

throw new ReservedFieldName('id')
```

## Query & Database Errors

### QueryError

For database query failures with path information.

```typescript
import { QueryError } from 'payload/errors'

throw new QueryError([{ path: 'users.email' }], req.t)
```

### NotFound

When requested resources don't exist.

```typescript
import { NotFound } from 'payload/errors'

throw new NotFound(req.t)
```

## Complete Error Class Reference

```typescript
// Authentication & Authorization
export class AuthenticationError extends APIError
export class Forbidden extends APIError  
export class UnauthorizedError extends APIError
export class LockedAuth extends APIError
export class UnverifiedEmail extends APIError
export class Locked extends APIError

// File Operations
export class FileUploadError extends APIError
export class FileRetrievalError extends APIError
export class ErrorDeletingFile extends APIError
export class MissingFile extends APIError

// Configuration & Development
export class InvalidConfiguration extends APIError
export class DuplicateCollection extends APIError
export class DuplicateGlobal extends APIError
export class DuplicateFieldName extends APIError
export class InvalidFieldName extends APIError
export class InvalidFieldRelationship extends APIError
export class InvalidFieldJoin extends APIError
export class ReservedFieldName extends APIError
export class MissingFieldType extends APIError
export class MissingFieldInputOptions extends APIError
export class MissingEditorProp extends APIError
export class MissingCollectionLabel extends APIError
export class InvalidSchema extends APIError
export class TimestampsRequired extends APIError

// Database & Queries
export class QueryError extends APIError<{ path: string }[]>
export class NotFound extends APIError

// Validation
export class ValidationError extends APIError<{
  collection?: string
  errors: ValidationFieldError[]
  global?: string
}>
```

## Error Formatting

PayloadCMS includes utilities for formatting errors consistently:

```typescript
import { formatErrors } from 'payload/utilities'
import { APIError } from 'payload/errors'

const error = new APIError('Something went wrong', 500, { details: 'Additional info' })
const formatted = formatErrors(error)

// Result:
// {
//   errors: [
//     {
//       name: 'APIError',
//       data: { details: 'Additional info' },
//       message: 'Something went wrong'
//     }
//   ]
// }
```

## TypeScript Types

```typescript
/**
 * Error names that can be thrown by Payload during runtime
 */
export type ErrorName =
  | 'APIError'
  | 'AuthenticationError'
  | 'ErrorDeletingFile'
  | 'FileRetrievalError'
  | 'FileUploadError'
  | 'Forbidden'
  | 'Locked'
  | 'LockedAuth'
  | 'MissingFile'
  | 'NotFound'
  | 'QueryError'
  | 'UnverifiedEmail'
  | 'ValidationError'

/**
 * Field-level validation error
 */
export type ValidationFieldError = {
  label?: LabelFunction | StaticLabel
  message: string
  path: string
}
```

## Usage in Hooks and Middleware

### Collection Hooks

```typescript
import { ValidationError } from 'payload/errors'

const MyCollection = {
  slug: 'users',
  hooks: {
    beforeValidate: [
      ({ data, req }) => {
        if (!data.email) {
          throw new ValidationError({
            errors: [{
              path: 'email',
              message: 'Email is required'
            }],
            collection: 'users'
          }, req.t)
        }
        return data
      }
    ]
  }
}
```

### API Routes

```typescript
import { Forbidden, APIError } from 'payload/errors'

export const myCustomEndpoint = async (req, res) => {
  try {
    if (!req.user) {
      throw new Forbidden(req.t)
    }
    
    // Your logic here
    
  } catch (error) {
    if (error instanceof APIError) {
      return res.status(error.status).json({
        errors: [{
          name: error.name,
          message: error.message,
          data: error.data
        }]
      })
    }
    
    // Handle other errors
    return res.status(500).json({
      errors: [{ message: 'Internal server error' }]
    })
  }
}
```

## Internationalization Support

Most error classes accept a translation function for multilingual support:

```typescript
import { AuthenticationError } from 'payload/errors'

// In a hook or endpoint with request context
throw new AuthenticationError(req.t) // Uses current locale

// Direct translation key usage
const message = req.t('error:emailOrPasswordIncorrect')
throw new APIError(message, 401)
```

## Common Patterns

### Input Validation

```typescript
import { ValidationError } from 'payload/errors'

const validateInput = (data, req) => {
  const errors = []
  
  if (!data.email) {
    errors.push({
      path: 'email',
      message: req.t('validation:required')
    })
  }
  
  if (!data.password || data.password.length < 8) {
    errors.push({
      path: 'password', 
      message: req.t('validation:minLength', { min: 8 })
    })
  }
  
  if (errors.length > 0) {
    throw new ValidationError({ errors }, req.t)
  }
}
```

### Permission Checking

```typescript
import { Forbidden } from 'payload/errors'

const checkPermission = (req, action, resource) => {
  if (!req.user) {
    throw new AuthenticationError(req.t)
  }
  
  if (!req.user.permissions[resource]?.includes(action)) {
    throw new Forbidden(req.t)
  }
}
```

### File Upload Validation

```typescript
import { FileUploadError, ValidationError } from 'payload/errors'

const validateFileUpload = (file, req) => {
  if (!file) {
    throw new ValidationError({
      errors: [{
        path: 'file',
        message: req.t('validation:fileRequired')
      }]
    }, req.t)
  }
  
  if (file.size > 10 * 1024 * 1024) { // 10MB
    throw new FileUploadError(req.t)
  }
}
```

## Error Handling Best Practices

1. **Use Specific Error Types**: Choose the most appropriate error class for the situation
2. **Include Relevant Data**: Add contextual information to help with debugging
3. **Consider User Visibility**: Use the `isPublic` parameter appropriately
4. **Internationalization**: Always pass the translation function when available
5. **Consistent Status Codes**: Use standard HTTP status codes for API responses

## Troubleshooting

### Common Issues

#### Error Not Being Caught

**Problem:** Custom errors aren't being handled by the error middleware

**Solution:** Ensure your errors extend `APIError` and are thrown (not returned)

```typescript
// ❌ Wrong
const handleError = () => {
  return new APIError('Error message')
}

// ✅ Correct  
const handleError = () => {
  throw new APIError('Error message')
}
```

#### Validation Errors Not Displaying

**Problem:** Validation errors aren't showing in the admin panel

**Solution:** Ensure validation errors include proper field paths and are thrown during the correct lifecycle

```typescript
// ✅ Correct usage in beforeValidate hook
beforeValidate: [
  ({ data, req }) => {
    if (!data.email) {
      throw new ValidationError({
        errors: [{ 
          path: 'email',  // Must match field name
          message: 'Email is required' 
        }]
      }, req.t)
    }
  }
]
```

#### Translation Not Working

**Problem:** Error messages not translating properly

**Solution:** Ensure translation context is passed correctly

```typescript
// ✅ Pass req.t when available
throw new AuthenticationError(req.t)

// ✅ Fallback for contexts without req
const t = req?.t || ((key) => key)
throw new AuthenticationError(t)
```

## Performance Considerations

- Error objects include stack traces which can impact performance in high-frequency scenarios
- Consider using error codes or types for programmatic error handling instead of message comparison
- Validation errors with many fields can become large; consider paginating or limiting error count

## Security Considerations

- Never expose sensitive data in error messages visible to end users
- Use `isPublic: false` (default) for errors containing internal information
- Sanitize user input before including in error messages
- Log security-related errors for monitoring purposes

## Contributing

Found a bug or have a suggestion? [Open an issue](https://github.com/payloadcms/payload/issues) or submit a Pull Request.

## License

MIT License - see the [LICENSE](https://github.com/payloadcms/payload/blob/main/LICENSE) file for details.