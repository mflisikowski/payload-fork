# PayloadCMS Authentication System

![NPM Version](https://img.shields.io/npm/v/payload)
![Bundle Size](https://img.shields.io/bundlephobia/minzip/payload)

## Overview

The PayloadCMS Authentication System is a comprehensive, secure authentication solution built into the core Payload framework. It provides robust user authentication, authorization, session management, and access control mechanisms designed for modern web applications. The system supports multiple authentication strategies including JWT tokens, API keys, and local username/password authentication with advanced security features like account lockouts, email verification, and password recovery.

This authentication system is engineered for enterprise-grade applications, offering fine-grained permissions, role-based access control, and seamless integration with PayloadCMS collections. It handles everything from basic user login/logout to complex multi-tenant authorization scenarios.

<Banner type="info">
The package is open-source. [View source code](https://github.com/payloadcms/payload/tree/main/packages/payload/src/auth). Need help? [Community Help](https://payloadcms.com/community-help).
</Banner>

## System Requirements

- **PayloadCMS**: ^3.54.0
- **Node.js**: ^18.20.2 || >=20.9.0
- **TypeScript**: ^5.0.0
- **Dependencies**: jose, bson-objectid, scmp, uuid

## Key Features

- 🔐 **Multiple Authentication Strategies** - JWT, API Keys, Local, Custom
- 🛡️ **Advanced Security** - Account lockouts, rate limiting, CSRF protection
- 📧 **Email Verification** - Optional email verification workflow
- 🔄 **Password Recovery** - Secure forgot/reset password functionality
- 👥 **Session Management** - HTTP-only cookie sessions with automatic cleanup
- 🎯 **Granular Permissions** - Field-level and document-level access control
- 🌍 **Multi-tenant Support** - Collection-based user isolation
- ⚡ **High Performance** - Optimized for scalability and speed

## Configuration

### Basic Setup

```typescript
import { CollectionConfig } from 'payload'

const Users: CollectionConfig = {
  slug: 'users',
  auth: {
    // Enable authentication for this collection
    tokenExpiration: 7200, // 2 hours
    verify: {
      generateEmailHTML: ({ token, user }) => {
        return `<a href="${process.env.PAYLOAD_PUBLIC_SERVER_URL}/verify-email?token=${token}">Verify Email</a>`
      },
    },
    forgotPassword: {
      generateEmailHTML: ({ token, user }) => {
        return `<a href="${process.env.PAYLOAD_PUBLIC_SERVER_URL}/reset-password?token=${token}">Reset Password</a>`
      },
    },
    maxLoginAttempts: 5,
    lockTime: 600000, // 10 minutes
  },
  fields: [
    {
      name: 'email',
      type: 'email',
      required: true,
      unique: true,
    },
    {
      name: 'role',
      type: 'select',
      options: ['admin', 'editor', 'user'],
      defaultValue: 'user',
    },
  ],
}
```

### Advanced Configuration

```typescript
import { CollectionConfig } from 'payload'
import { AuthStrategy } from 'payload'

// Custom authentication strategy
const customAuthStrategy: AuthStrategy = {
  name: 'oauth',
  authenticate: async ({ headers, payload }) => {
    // Custom OAuth implementation
    const token = headers.get('Authorization')?.replace('Bearer ', '')
    if (!token) return { user: null }
    
    // Validate token with OAuth provider
    const user = await validateOAuthToken(token)
    return { user }
  }
}

const Users: CollectionConfig = {
  slug: 'users',
  auth: {
    // Security settings
    tokenExpiration: 3600, // 1 hour
    useAPIKey: true,
    maxLoginAttempts: 3,
    lockTime: 900000, // 15 minutes
    
    // Cookie configuration
    cookies: {
      secure: process.env.NODE_ENV === 'production',
      sameSite: 'Strict',
      domain: process.env.COOKIE_DOMAIN,
    },
    
    // Username login support
    loginWithUsername: {
      allowEmailLogin: true,
      requireEmail: false,
      requireUsername: true,
    },
    
    // Custom strategies
    strategies: [customAuthStrategy],
    
    // Session management
    useSessions: true,
    depth: 1, // How deep to populate user data in JWT
    
    // Email verification
    verify: {
      generateEmailHTML: ({ token, user, req }) => {
        return `
          <h1>Verify Your Email</h1>
          <p>Hello ${user.email},</p>
          <p>Click the link below to verify your email address:</p>
          <a href="${req.payload.config.serverURL}/api/users/verify/${user.id}?token=${token}">
            Verify Email Address
          </a>
        `
      },
      generateEmailSubject: ({ user }) => `Verify your account, ${user.email}`,
    },
    
    // Password recovery
    forgotPassword: {
      expiration: 3600000, // 1 hour
      generateEmailHTML: ({ token, user }) => {
        return `
          <h1>Reset Your Password</h1>
          <p>You requested a password reset. Click the link below to set a new password:</p>
          <a href="${process.env.CLIENT_URL}/reset-password?token=${token}">Reset Password</a>
          <p>This link expires in 1 hour.</p>
        `
      },
    },
  },
  fields: [
    {
      name: 'email',
      type: 'email',
      required: true,
      unique: true,
    },
    {
      name: 'username',
      type: 'text',
      unique: true,
    },
    {
      name: 'role',
      type: 'select',
      options: [
        { label: 'Admin', value: 'admin' },
        { label: 'Editor', value: 'editor' },
        { label: 'User', value: 'user' },
      ],
      defaultValue: 'user',
      access: {
        update: ({ req: { user } }) => {
          return user?.role === 'admin'
        },
      },
    },
  ],
}
```

## API Reference

### Authentication Operations

#### `login(args)`

Authenticates a user with email/username and password.

**Parameters:**
- `collection`: Collection configuration
- `data`: Login credentials (`{ email?, username?, password }`)
- `depth?`: Population depth for user data
- `req`: PayloadRequest object

**Returns:** `Promise<{ user, token, exp }>`

**Example:**
```typescript
const result = await payload.auth.login({
  collection: 'users',
  data: {
    email: 'user@example.com',
    password: 'securePassword123',
  },
  req,
})

console.log(result.user) // Authenticated user object
console.log(result.token) // JWT token
console.log(result.exp) // Token expiration timestamp
```

#### `logout(args)`

Logs out the current user and invalidates their session.

**Parameters:**
- `collection`: Collection configuration
- `req`: PayloadRequest object

**Example:**
```typescript
await payload.auth.logout({
  collection: 'users',
  req,
})
```

#### `forgotPassword(args)`

Initiates password recovery process by sending reset email.

**Parameters:**
- `collection`: Collection configuration
- `data`: `{ email }` or `{ username }`
- `req`: PayloadRequest object

**Example:**
```typescript
await payload.auth.forgotPassword({
  collection: 'users',
  data: { email: 'user@example.com' },
  req,
})
```

#### `resetPassword(args)`

Resets user password using a valid reset token.

**Parameters:**
- `collection`: Collection configuration
- `data`: `{ token, password }`
- `req`: PayloadRequest object

**Example:**
```typescript
await payload.auth.resetPassword({
  collection: 'users',
  data: {
    token: 'reset-token-here',
    password: 'newSecurePassword123',
  },
  req,
})
```

### Cookie Management Functions

#### `generatePayloadCookie(args)`

Generates secure HTTP-only authentication cookies.

**Parameters:**
- `collectionAuthConfig`: Auth configuration
- `cookiePrefix`: Cookie name prefix
- `token`: JWT token
- `returnCookieAsObject?`: Return format preference

**Returns:** Cookie string or object

**Example:**
```typescript
import { generatePayloadCookie } from 'payload'

const cookie = generatePayloadCookie({
  collectionAuthConfig: collection.config.auth,
  cookiePrefix: 'payload',
  token: jwtToken,
})

response.headers.set('Set-Cookie', cookie)
```

#### `parseCookies(headers)`

Parses HTTP Cookie header into a Map.

**Parameters:**
- `headers`: Request headers object

**Returns:** `Map<string, string>`

**Example:**
```typescript
import { parseCookies } from 'payload'

const cookies = parseCookies(request.headers)
const authToken = cookies.get('payload-token')
```

### JWT Utilities

#### `extractJWT(args)`

Extracts JWT token from request headers or cookies.

**Parameters:**
- `headers`: Request headers
- `payload`: Payload instance

**Returns:** JWT token string or null

**Example:**
```typescript
import { extractJWT } from 'payload'

const token = extractJWT({
  headers: request.headers,
  payload,
})
```

### Authentication Strategies

#### JWT Strategy

Built-in JWT authentication with session support.

```typescript
import { JWTAuthentication } from 'payload'

// JWT strategy is automatically registered
const authResult = await JWTAuthentication({
  headers: request.headers,
  payload,
  strategyName: 'local-jwt',
})
```

#### API Key Strategy

API key-based authentication for programmatic access.

```typescript
// Enable API keys in collection config
const Users: CollectionConfig = {
  slug: 'users',
  auth: {
    useAPIKey: true,
  },
}

// API key will be automatically generated for users
// Use in requests: Authorization: Bearer <api-key>
```

#### Custom Strategy

Implement custom authentication logic.

```typescript
import { AuthStrategy } from 'payload'

const customStrategy: AuthStrategy = {
  name: 'custom-oauth',
  authenticate: async ({ headers, payload, canSetHeaders }) => {
    const token = headers.get('Authorization')?.replace('Bearer ', '')
    
    if (!token) {
      return { user: null }
    }
    
    try {
      // Validate with external service
      const userData = await validateWithOAuth(token)
      
      // Find or create user in Payload
      const user = await payload.findOne({
        collection: 'users',
        where: { email: { equals: userData.email } }
      })
      
      return {
        user: user || null,
        responseHeaders: canSetHeaders ? new Headers() : undefined,
      }
    } catch (error) {
      return { user: null }
    }
  },
}

// Register in collection config
const Users: CollectionConfig = {
  auth: {
    strategies: [customStrategy],
  },
}
```

## TypeScript Types

```typescript
// Core authentication types
export interface Auth {
  cookies: {
    domain?: string
    sameSite: 'Lax' | 'None' | 'Strict'
    secure: boolean
  }
  depth: number
  disableLocalStrategy: boolean | { enableFields?: boolean; optionalPassword?: boolean }
  forgotPassword?: {
    expiration: number
    generateEmailHTML?: (args: { req: PayloadRequest; token: string; user: any }) => string
    generateEmailSubject?: (args: { req: PayloadRequest; token: string; user: any }) => string
  }
  lockTime: number
  loginWithUsername: false | LoginWithUsernameOptions
  maxLoginAttempts: number
  removeTokenFromResponses?: boolean
  strategies: AuthStrategy[]
  tokenExpiration: number
  useAPIKey: boolean
  useSessions: boolean
  verify?: boolean | {
    generateEmailHTML?: (args: { req: PayloadRequest; token: string; user: any }) => string
    generateEmailSubject?: (args: { req: PayloadRequest; token: string; user: any }) => string
  }
}

// Permission types
export type Permission = {
  permission: boolean
  where?: Where
}

export type CollectionPermission = {
  create: Permission
  delete: Permission
  fields: FieldsPermissions
  read: Permission
  readVersions?: Permission
  update: Permission
}

export type Permissions = {
  canAccessAdmin: boolean
  collections?: Record<string, CollectionPermission>
  globals?: Record<string, GlobalPermission>
}

// User types
export type ClientUser = {
  id: string | number
  email?: string
  username?: string
  sessions?: UserSession[]
  [key: string]: any
}

export type UserSession = {
  id: string
  createdAt: Date | string
  expiresAt: Date | string
}

// Strategy types
export type AuthStrategyFunction = (args: {
  headers: Headers
  payload: Payload
  strategyName?: string
  canSetHeaders?: boolean
  isGraphQL?: boolean
}) => Promise<AuthStrategyResult>

export type AuthStrategyResult = {
  user: (TypedUser & { _strategy?: string; collection?: string }) | null
  responseHeaders?: Headers
}

export type AuthStrategy = {
  name: string
  authenticate: AuthStrategyFunction
}
```

## Usage Guides

### Basic User Authentication

```typescript
// 1. Set up user collection with auth
const Users: CollectionConfig = {
  slug: 'users',
  auth: true, // Enable with defaults
  fields: [
    {
      name: 'email',
      type: 'email',
      required: true,
    },
  ],
}

// 2. Login endpoint usage
app.post('/login', async (req, res) => {
  try {
    const result = await payload.auth.login({
      collection: 'users',
      data: req.body, // { email, password }
      req: req as PayloadRequest,
    })
    
    // Set auth cookie
    const cookie = generatePayloadCookie({
      collectionAuthConfig: Users.auth,
      cookiePrefix: 'payload',
      token: result.token,
    })
    
    res.setHeader('Set-Cookie', cookie)
    res.json({ user: result.user })
  } catch (error) {
    res.status(401).json({ error: error.message })
  }
})
```

### Email Verification Workflow

```typescript
// 1. Configure email verification
const Users: CollectionConfig = {
  slug: 'users',
  auth: {
    verify: {
      generateEmailHTML: ({ token, user }) => `
        <h1>Verify Email</h1>
        <p>Hello ${user.email},</p>
        <p>Click to verify: <a href="${process.env.CLIENT_URL}/verify?token=${token}">Verify</a></p>
      `,
      generateEmailSubject: () => 'Please verify your email',
    },
  },
}

// 2. Handle verification in your app
app.get('/verify', async (req, res) => {
  try {
    await payload.auth.verifyEmail({
      collection: 'users',
      token: req.query.token,
      req: req as PayloadRequest,
    })
    res.redirect('/login?verified=true')
  } catch (error) {
    res.redirect('/login?error=verification-failed')
  }
})
```

### Role-Based Access Control

```typescript
const Users: CollectionConfig = {
  slug: 'users',
  auth: true,
  access: {
    // Only admins can read all users
    read: ({ req: { user } }) => {
      if (user?.role === 'admin') return true
      return { id: { equals: user?.id } } // Users can only read themselves
    },
    update: ({ req: { user }, id }) => {
      if (user?.role === 'admin') return true
      return user?.id === id // Users can only update themselves
    },
    delete: ({ req: { user } }) => user?.role === 'admin',
  },
  fields: [
    {
      name: 'role',
      type: 'select',
      options: ['admin', 'editor', 'user'],
      access: {
        update: ({ req: { user } }) => user?.role === 'admin',
      },
    },
  ],
}
```

### API Key Authentication

```typescript
// 1. Enable API keys
const Users: CollectionConfig = {
  slug: 'users',
  auth: {
    useAPIKey: true,
  },
}

// 2. Use API key in requests
const response = await fetch('/api/protected-endpoint', {
  headers: {
    'Authorization': `Bearer ${apiKey}`,
    'Content-Type': 'application/json',
  },
})

// 3. Generate API key for user
const user = await payload.update({
  collection: 'users',
  id: userId,
  data: {
    enableAPIKey: true,
  },
})

console.log(user.apiKey) // Generated API key
```

### Session Management

```typescript
// Configure session-based auth
const Users: CollectionConfig = {
  slug: 'users',
  auth: {
    useSessions: true,
    tokenExpiration: 86400, // 24 hours
  },
}

// Check user sessions
const userWithSessions = await payload.findByID({
  collection: 'users',
  id: userId,
})

console.log(userWithSessions.sessions) // Array of active sessions

// Clear all user sessions
await payload.update({
  collection: 'users',
  id: userId,
  data: {
    sessions: [], // Clears all sessions
  },
})
```

## Security Features

### Account Lockout Protection

```typescript
const Users: CollectionConfig = {
  slug: 'users',
  auth: {
    maxLoginAttempts: 5, // Lock after 5 failed attempts
    lockTime: 600000, // Lock for 10 minutes (in milliseconds)
  },
}
```

### CSRF Protection

PayloadCMS automatically includes CSRF protection through:
- HTTP-only cookies for session tokens
- SameSite cookie attributes
- Origin header validation

### Secure Cookie Configuration

```typescript
const Users: CollectionConfig = {
  slug: 'users',
  auth: {
    cookies: {
      secure: process.env.NODE_ENV === 'production', // HTTPS only in production
      sameSite: 'Strict', // Prevent cross-site requests
      domain: process.env.COOKIE_DOMAIN, // Restrict cookie domain
    },
  },
}
```

## Performance Optimization

### JWT Payload Optimization

```typescript
const Users: CollectionConfig = {
  slug: 'users',
  auth: {
    depth: 0, // Don't populate relationships in JWT (better performance)
  },
}
```

### Database Query Optimization

```typescript
// Use specific field selection for auth queries
const user = await payload.db.findOne({
  collection: 'users',
  select: {
    id: true,
    email: true,
    role: true,
    // Only select needed fields
  },
  where: { email: { equals: userEmail } },
})
```

## Troubleshooting

### Common Issues

#### "Invalid token" Error
**Problem:** JWT token validation fails

**Solution:**
1. Check token expiration
2. Verify JWT secret consistency
3. Ensure cookie domain/path settings

```typescript
// Debug JWT issues
import { jwtVerify } from 'jose'

try {
  const { payload } = await jwtVerify(token, new TextEncoder().encode(secret))
  console.log('Token valid:', payload)
} catch (error) {
  console.error('Token invalid:', error.message)
}
```

#### Account Lockout Issues
**Problem:** User locked out unexpectedly

**Solution:**
```typescript
// Manually unlock user
await payload.update({
  collection: 'users',
  id: userId,
  data: {
    loginAttempts: 0,
    lockUntil: undefined,
  },
})
```

#### Email Verification Not Working
**Problem:** Verification emails not sending

**Solution:**
1. Check email configuration
2. Verify SMTP settings
3. Check spam folders

```typescript
// Test email configuration
await payload.sendEmail({
  to: 'test@example.com',
  subject: 'Test Email',
  text: 'Test email content',
})
```

### Debugging

Enable debug logging for authentication:

```typescript
// In your payload config
export default buildConfig({
  // ... other config
  debug: process.env.NODE_ENV === 'development',
  loggerOptions: {
    level: 'debug',
  },
})
```

## Migration Guide

### From v2 to v3

Key breaking changes in authentication:

1. **Strategy Registration**: Custom strategies now registered differently
2. **Cookie Handling**: Updated cookie generation API
3. **TypeScript Types**: Updated user types and interfaces

```typescript
// v2 (Old)
const customStrategy = {
  name: 'custom',
  authenticate: ({ req }) => { /* ... */ }
}

// v3 (New)
const customStrategy: AuthStrategy = {
  name: 'custom',
  authenticate: ({ headers, payload }) => { /* ... */ }
}
```

## Example Projects

- [Basic Auth Setup](https://github.com/payloadcms/payload/tree/main/examples/auth) - Simple email/password authentication
- [Role-Based Access](https://github.com/payloadcms/payload/tree/main/examples/custom-components) - Advanced permission system
- [API Key Integration](https://github.com/payloadcms/payload/tree/main/examples/api-keys) - Programmatic API access

## Contributing

Found a bug or have a suggestion? [Open an issue](https://github.com/payloadcms/payload/issues) or submit a Pull Request.

## License

MIT License - see the [LICENSE](https://github.com/payloadcms/payload/blob/main/LICENSE) file for details.