---
title: Email Core Module
label: Email Core
order: 10
desc: Internal email adapter system providing console logging, type definitions, and utilities for PayloadCMS email functionality.
keywords: [email, adapter, console, types, payload, nodemailer, sendmail, logging, utilities]
---

<Banner type="warning">
**Original Documentation**: The content below comes from [official PayloadCMS documentation](../../../docs/email/overview.mdx).
Further in the document, you'll find an extended, more detailed version of this documentation.
</Banner>

## Introduction

Payload has a few email adapters that can be imported to enable email functionality. The [@payloadcms/email-nodemailer](https://www.npmjs.com/package/@payloadcms/email-nodemailer) package will be the package most will want to install. This package provides an easy way to use [Nodemailer](https://nodemailer.com) for email and won't get in your way for those already familiar.

The email adapter should be passed into the `email` property of the Payload Config. This will allow Payload to send [auth-related emails](../authentication/email) for things like password resets, new user verification, and any other email sending needs you may have.

## Configuration

### Default Configuration

When email is not needed or desired, Payload will log a warning on startup notifying that email is not configured. A warning message will also be logged on any attempt to send an email.

### Email Adapter

An email adapter will require at least the following fields:

| Option                      | Description                                                                      |
| --------------------------- | -------------------------------------------------------------------------------- |
| **`defaultFromName`** \*    | The name part of the From field that will be seen on the delivered email         |
| **`defaultFromAddress`** \* | The email address part of the From field that will be used when delivering email |

### Official Email Adapters

| Name       | Package                                                                                    | Description                                                                                                                                                                                     |
| ---------- | ------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Nodemailer | [@payloadcms/email-nodemailer](https://www.npmjs.com/package/@payloadcms/email-nodemailer) | Use any [Nodemailer transport](https://nodemailer.com/transports), including SMTP, Resend, SendGrid, and more. This was provided by default in Payload 2.x. This is the easiest migration path. |
| Resend     | [@payloadcms/email-resend](https://www.npmjs.com/package/@payloadcms/email-resend)         | Resend email via their REST API. This is preferred for serverless platforms such as Vercel because it is much more lightweight than the nodemailer adapter.                                     |

## Nodemailer Configuration

| Option                 | Description                                                                                                                                                                            |
| ---------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **`transport`**        | The Nodemailer transport object for when you want to do it yourself, not needed when transportOptions is set                                                                           |
| **`transportOptions`** | An object that configures the transporter that Payload will create. For all the available options see the [Nodemailer documentation](https://nodemailer.com) or see the examples below |

## Use SMTP

Simple Mail Transfer Protocol (SMTP) options can be passed in using the `transportOptions` object on the `email` options. See the [Nodemailer SMTP documentation](https://nodemailer.com/smtp/) for more information, including details on when `secure` should and should not be set to `true`.

**Example email options using SMTP:**

```ts
import { buildConfig } from 'payload'
import { nodemailerAdapter } from '@payloadcms/email-nodemailer'

export default buildConfig({
  email: nodemailerAdapter({
    defaultFromAddress: 'info@payloadcms.com',
    defaultFromName: 'Payload',
    // Nodemailer transportOptions
    transportOptions: {
      host: process.env.SMTP_HOST,
      port: 587,
      auth: {
        user: process.env.SMTP_USER,
        pass: process.env.SMTP_PASS,
      },
    },
  }),
})
```

**Example email options using nodemailer.createTransport:**

```ts
import { buildConfig } from 'payload'
import { nodemailerAdapter } from '@payloadcms/email-nodemailer'
import nodemailer from 'nodemailer'

export default buildConfig({
  email: nodemailerAdapter({
    defaultFromAddress: 'info@payloadcms.com',
    defaultFromName: 'Payload',
    // Any Nodemailer transport can be used
    transport: nodemailer.createTransport({
      host: process.env.SMTP_HOST,
      port: 587,
      auth: {
        user: process.env.SMTP_USER,
        pass: process.env.SMTP_PASS,
      },
    }),
  }),
})
```

**Custom Transport:**

You also have the ability to bring your own nodemailer transport. This is an example of using the SendGrid nodemailer transport.

```ts
import { buildConfig } from 'payload'
import { nodemailerAdapter } from '@payloadcms/email-nodemailer'
import nodemailerSendgrid from 'nodemailer-sendgrid'

export default buildConfig({
  email: nodemailerAdapter({
    defaultFromAddress: 'info@payloadcms.com',
    defaultFromName: 'Payload',
    transportOptions: nodemailerSendgrid({
      apiKey: process.env.SENDGRID_API_KEY,
    }),
  }),
})
```

During development, if you pass nothing to `nodemailerAdapter`, it will use the [ethereal.email](https://ethereal.email) service.

This will log the ethereal.email details to console on startup.

```ts
import { nodemailerAdapter } from '@payloadcms/email-nodemailer'

export default buildConfig({
  email: nodemailerAdapter(),
})
```

## Resend Configuration

The Resend adapter requires an API key to be passed in the options. This can be found in the Resend dashboard. This is the preferred package if you are deploying on Vercel because this is much more lightweight than the Nodemailer adapter.

| Option | Description                         |
| ------ | ----------------------------------- |
| apiKey | The API key for the Resend service. |

```ts
import { buildConfig } from 'payload'
import { resendAdapter } from '@payloadcms/email-resend'

export default buildConfig({
  email: resendAdapter({
    defaultFromAddress: 'dev@payloadcms.com',
    defaultFromName: 'Payload CMS',
    apiKey: process.env.RESEND_API_KEY || '',
  }),
})
```

## Sending Mail

With a working transport you can call it anywhere you have access to Payload by calling `payload.sendEmail(message)`. The `message` will contain the `to`, `subject` and `html` or `text` for the email being sent. Other options are also available and can be seen in the sendEmail args. Support for these will depend on the adapter being used.

```ts
// Example of sending an email
const email = await payload.sendEmail({
  to: 'test@example.com',
  subject: 'This is a test email',
  text: 'This is my message body',
})
```

## Using multiple mail providers

Payload supports the use of a single transporter of email, but there is nothing stopping you from having more. Consider a use case where sending bulk email is handled differently than transactional email and could be done using a [hook](/docs/hooks/overview).

---

## 📚 Extended Documentation

<Banner type="success">
**Note**: The documentation below has been automatically generated based on source code analysis and contains more detailed information than the original documentation above.
</Banner>

## Detailed Overview

The PayloadCMS Email Core Module provides the foundational infrastructure for email functionality within PayloadCMS. This internal package serves as the backbone for email communication, offering a flexible adapter pattern that supports various email service providers while maintaining a consistent interface.

The core module includes type definitions, default configurations, utility functions, and a console-based fallback adapter that ensures proper error handling and logging when email services are not configured. It's designed to work seamlessly with external email adapters like Nodemailer and Resend while providing developers with the flexibility to create custom email solutions.

Key benefits include a consistent API across different email providers, built-in fallback mechanisms for development environments, comprehensive TypeScript support for type safety, and utility functions for common email operations like address formatting.

<Banner type="info">
The package is open-source. [View source code](https://github.com/payloadcms/payload/tree/main/packages/payload/src/email). Need help? [Community Help](https://payloadcms.com/community-help).
</Banner>

## System Requirements

- **PayloadCMS**: ^3.0.0
- **Node.js**: >=18.0.0
- **TypeScript**: ^5.0.0 (recommended for type safety)

## Installation

The email core module is included automatically with PayloadCMS and doesn't require separate installation:

```bash
# npm
npm install payload

# yarn  
yarn add payload

# pnpm
pnpm add payload
```

## Quick Start

The email core is used internally by PayloadCMS. For external usage, you'll typically work with email adapters:

```typescript
import { buildConfig } from 'payload'
import { consoleEmailAdapter } from 'payload'

// Basic console adapter for development
export default buildConfig({
  email: consoleEmailAdapter({ payload }),
  // ... other config
})
```

## Detailed Configuration

### Main Types

#### `EmailAdapter<TSendEmailResponse>`

- **Type**: `({ payload }: { payload: Payload }) => InitializedEmailAdapter<TSendEmailResponse>`
- **Required**: Yes
- **Description**: The main interface for creating email adapters

The EmailAdapter type defines the contract that all email adapters must implement. It takes a generic type parameter for the response type returned by the sendEmail method.

```typescript
import type { EmailAdapter } from 'payload'

const customAdapter: EmailAdapter<{ messageId: string }> = ({ payload }) => ({
  name: 'custom-adapter',
  defaultFromAddress: 'noreply@example.com',
  defaultFromName: 'My App',
  sendEmail: async (message) => {
    // Custom email sending logic
    return { messageId: 'custom-id-123' }
  }
})
```

#### `SendEmailOptions`

- **Type**: `Prettify<NodemailerSendMailOptions>`
- **Description**: Email message options extending Nodemailer's SendMailOptions

Defines the structure for email messages that can be sent through any adapter.

```typescript
import type { SendEmailOptions } from 'payload'

const emailMessage: SendEmailOptions = {
  to: 'user@example.com',
  from: 'noreply@example.com', 
  subject: 'Welcome to our platform',
  html: '<h1>Welcome!</h1><p>Thanks for joining us.</p>',
  text: 'Welcome! Thanks for joining us.',
  attachments: [
    {
      filename: 'welcome.pdf',
      content: Buffer.from('...'),
      contentType: 'application/pdf'
    }
  ]
}
```

#### `InitializedEmailAdapter<TSendEmailResponse>`

- **Type**: `ReturnType<EmailAdapter<TSendEmailResponse>>`
- **Description**: The initialized adapter instance used internally by Payload

This represents an email adapter after it has been initialized with the Payload instance.

### Configuration Schema

```typescript
// Core email adapter interface
interface EmailAdapter<TSendEmailResponse = unknown> {
  ({ payload }: { payload: Payload }): {
    name: string
    defaultFromAddress: string
    defaultFromName: string
    sendEmail: (message: SendEmailOptions) => Promise<TSendEmailResponse>
  }
}

// Email options interface
interface SendEmailOptions extends NodemailerSendMailOptions {
  to: string | string[] | Address | Address[]
  from?: string | Address
  subject: string
  text?: string
  html?: string
  attachments?: Attachment[]
  // ... other Nodemailer options
}

// Default configuration
interface EmailDefaults {
  defaultFromAddress: string
  defaultFromName: string
}
```

## Usage Guides

### Creating a Custom Email Adapter

Here's how to create a custom email adapter that integrates with a third-party email service:

```typescript
import type { EmailAdapter, SendEmailOptions } from 'payload'

interface CustomEmailResponse {
  id: string
  status: 'sent' | 'failed'
}

export const customEmailAdapter: EmailAdapter<CustomEmailResponse> = ({ payload }) => ({
  name: 'custom-email-service',
  defaultFromAddress: 'noreply@myapp.com',
  defaultFromName: 'My Application',
  
  sendEmail: async (message: SendEmailOptions): Promise<CustomEmailResponse> => {
    try {
      // Log email attempt
      payload.logger.info({
        msg: `Sending email via custom service to ${message.to}`,
        subject: message.subject
      })

      // Custom email sending logic
      const response = await fetch('https://api.customemailservice.com/send', {
        method: 'POST',
        headers: {
          'Authorization': `Bearer ${process.env.CUSTOM_EMAIL_API_KEY}`,
          'Content-Type': 'application/json'
        },
        body: JSON.stringify({
          to: message.to,
          from: message.from,
          subject: message.subject,
          html: message.html,
          text: message.text
        })
      })

      if (!response.ok) {
        throw new Error(`Email service responded with ${response.status}`)
      }

      const result = await response.json()
      
      payload.logger.info({
        msg: `Email sent successfully`,
        messageId: result.id
      })

      return {
        id: result.id,
        status: 'sent'
      }
    } catch (error) {
      payload.logger.error({
        msg: `Failed to send email: ${error.message}`,
        error
      })
      
      return {
        id: '',
        status: 'failed'
      }
    }
  }
})
```

### Using the Console Email Adapter

For development and testing environments, use the built-in console adapter:

```typescript
import { buildConfig } from 'payload'
import { consoleEmailAdapter } from 'payload'

export default buildConfig({
  // Console adapter logs email attempts to console
  email: consoleEmailAdapter,
  
  // ... other configuration
})
```

### Advanced Patterns

#### Email Adapter with Retry Logic

```typescript
import type { EmailAdapter, SendEmailOptions } from 'payload'

export const retryEmailAdapter: EmailAdapter<{ attempts: number, success: boolean }> = ({ payload }) => ({
  name: 'retry-email-adapter',
  defaultFromAddress: 'noreply@example.com',
  defaultFromName: 'Reliable Mailer',
  
  sendEmail: async (message: SendEmailOptions) => {
    const maxAttempts = 3
    let attempts = 0
    
    while (attempts < maxAttempts) {
      attempts++
      
      try {
        // Simulate email sending with potential failure
        const success = Math.random() > 0.3 // 70% success rate
        
        if (success) {
          payload.logger.info({
            msg: `Email sent successfully on attempt ${attempts}`,
            to: message.to,
            subject: message.subject
          })
          
          return { attempts, success: true }
        } else {
          throw new Error('Simulated email failure')
        }
      } catch (error) {
        payload.logger.warn({
          msg: `Email attempt ${attempts} failed: ${error.message}`,
          to: message.to,
          retriesLeft: maxAttempts - attempts
        })
        
        if (attempts === maxAttempts) {
          payload.logger.error({
            msg: `All ${maxAttempts} email attempts failed`,
            to: message.to,
            subject: message.subject
          })
          
          return { attempts, success: false }
        }
        
        // Wait before retry
        await new Promise(resolve => setTimeout(resolve, 1000 * attempts))
      }
    }
    
    return { attempts, success: false }
  }
})
```

## API Reference

### Functions

#### `getStringifiedToAddress(message: SendEmailOptions)`

Utility function that converts various "to" address formats into a readable string representation.

**Parameters:**
| Parameter | Type | Description |
|-----------|------|-------------|
| `message` | `SendEmailOptions` | Email message containing the "to" field |

**Returns:** `string | undefined`

**Example:**
```typescript
import { getStringifiedToAddress } from 'payload/email'

const message = {
  to: ['user1@example.com', { address: 'user2@example.com', name: 'User Two' }],
  subject: 'Test Email',
  text: 'Hello'
}

const stringified = getStringifiedToAddress(message)
// Returns: "user1@example.com, user2@example.com"
```

#### `consoleEmailAdapter({ payload })`

Built-in console adapter that logs email attempts instead of sending actual emails.

**Parameters:**
| Parameter | Type | Description |
|-----------|------|-------------|
| `payload` | `Payload` | The Payload CMS instance |

**Returns:** `InitializedEmailAdapter<void>`

**Example:**
```typescript
import { consoleEmailAdapter } from 'payload'

const adapter = consoleEmailAdapter({ payload })
await adapter.sendEmail({
  to: 'test@example.com',
  subject: 'Test',
  text: 'Hello world'
})
// Logs: "Email attempted without being configured. To: 'test@example.com', Subject: 'Test'"
```

### TypeScript Types

```typescript
// Main email adapter type
type EmailAdapter<TSendEmailResponse = unknown> = ({ payload }: { payload: Payload }) => {
  defaultFromAddress: string
  defaultFromName: string
  name: string
  sendEmail: (message: SendEmailOptions) => Promise<TSendEmailResponse>
}

// Initialized adapter type
type InitializedEmailAdapter<TSendEmailResponse = unknown> = ReturnType<
  EmailAdapter<TSendEmailResponse>
>

// Email options extending Nodemailer
type SendEmailOptions = Prettify<NodemailerSendMailOptions>

// Utility type for clean object representation
type Prettify<T> = {
  [K in keyof T]: T[K]
} & NonNullable<unknown>
```

## Integrations

### PayloadCMS Hooks

The email core module integrates with PayloadCMS authentication hooks:

- **User Verification**: Automatically sends verification emails when new users register
- **Password Reset**: Sends password reset emails when users request password changes
- **Collection Hooks**: Can be used in collection hooks for custom email notifications

### Database

The email core module doesn't directly interact with the database but relies on:

- **User Collections**: Accesses user email addresses for authentication-related emails
- **Configuration Storage**: Reads email settings from the PayloadCMS configuration

### External Services

The core module serves as an interface layer for:

- **Nodemailer**: Primary integration for SMTP-based email services
- **Resend**: Lightweight API-based email service integration
- **Custom Services**: Flexible adapter pattern supports any email service provider

## Troubleshooting

### Common Issues

#### Email Not Configured Warning

**Problem:** Console shows warnings about email not being configured, and no emails are sent.

**Solution:**
1. Verify that an email adapter is configured in your Payload config
2. Ensure the adapter is properly initialized
3. Check that required environment variables are set

**Example:**
```typescript
import { buildConfig } from 'payload'
import { nodemailerAdapter } from '@payloadcms/email-nodemailer'

export default buildConfig({
  email: nodemailerAdapter({
    defaultFromAddress: process.env.FROM_EMAIL,
    defaultFromName: process.env.FROM_NAME,
    transportOptions: {
      // ... your transport config
    }
  }),
})
```

#### Type Errors with Custom Adapters

**Problem:** TypeScript errors when creating custom email adapters.

**Solution:**
Ensure your adapter implements the correct interface with proper typing:

**Example:**
```typescript
import type { EmailAdapter } from 'payload'

// Specify the response type generic
const myAdapter: EmailAdapter<{ messageId: string }> = ({ payload }) => ({
  name: 'my-adapter',
  defaultFromAddress: 'test@example.com',
  defaultFromName: 'Test',
  sendEmail: async (message) => {
    // Implementation must return the specified type
    return { messageId: 'abc123' }
  }
})
```

#### Console Adapter in Production

**Problem:** Emails are being logged to console instead of being sent in production.

**Solution:**
Replace the console adapter with a proper email service adapter:

**Example:**
```typescript
// ❌ Wrong - using console adapter in production
email: consoleEmailAdapter

// ✅ Correct - using proper email service
email: nodemailerAdapter({
  defaultFromAddress: 'noreply@myapp.com',
  defaultFromName: 'My App',
  transportOptions: {
    // Production SMTP settings
  }
})
```

### Debugging

Enable debug logging to troubleshoot email issues:

```typescript
export default buildConfig({
  email: customAdapter,
  logger: {
    level: 'debug' // Enable detailed logging
  }
})
```

Check the console output for detailed information about email attempts, failures, and adapter initialization.

## Performance

### Performance Optimization

1. **Connection Pooling**: Use email services that support connection pooling for high-volume applications
2. **Async Processing**: Consider using job queues for non-critical emails to avoid blocking request processing
3. **Error Handling**: Implement proper error handling to prevent email failures from affecting user experience

```typescript
const optimizedAdapter: EmailAdapter = ({ payload }) => ({
  name: 'optimized-adapter',
  defaultFromAddress: 'noreply@example.com',
  defaultFromName: 'Optimized App',
  
  sendEmail: async (message) => {
    // Non-blocking email sending
    setImmediate(async () => {
      try {
        await actualEmailSending(message)
      } catch (error) {
        payload.logger.error('Background email failed', error)
      }
    })
    
    // Return immediately
    return { queued: true }
  }
})
```

## Security

### Security Best Practices

1. **Environment Variables**: Store email service credentials in environment variables, never in code
2. **Input Validation**: Validate email addresses and content before sending
3. **Rate Limiting**: Implement rate limiting to prevent email abuse
4. **Sanitization**: Sanitize HTML content in emails to prevent XSS attacks

```typescript
import validator from 'validator'

const secureAdapter: EmailAdapter = ({ payload }) => ({
  name: 'secure-adapter',
  defaultFromAddress: 'noreply@example.com',
  defaultFromName: 'Secure App',
  
  sendEmail: async (message) => {
    // Validate email addresses
    const toAddresses = Array.isArray(message.to) ? message.to : [message.to]
    for (const addr of toAddresses) {
      const email = typeof addr === 'string' ? addr : addr.address
      if (!validator.isEmail(email)) {
        throw new Error(`Invalid email address: ${email}`)
      }
    }
    
    // Sanitize HTML content
    if (message.html) {
      message.html = sanitizeHtml(message.html)
    }
    
    // Send email with validated and sanitized content
    return await sendSecureEmail(message)
  }
})
```

## Contributing

Found a bug or have a suggestion? [Open an issue](https://github.com/payloadcms/payload/issues) or submit a Pull Request.

## License

MIT License - see the [LICENSE](https://github.com/payloadcms/payload/blob/main/LICENSE) file for details.