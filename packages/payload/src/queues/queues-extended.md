---
title: Jobs Queue Core Module
label: Jobs Queue Core
order: 10
desc: Internal PayloadCMS module providing comprehensive job queue infrastructure, task orchestration, and workflow management for background processing.
keywords: [jobs, queue, tasks, workflows, scheduling, background, processing, cron, workers, async]
---

<Banner type="warning">
**Original Documentation**: The content below comes from [official PayloadCMS documentation](../../../docs/jobs-queue/overview.mdx).
Further in the document, you'll find an extended, more detailed version of this documentation.
</Banner>

Payload's Jobs Queue gives you a simple, yet powerful way to offload large or future tasks to separate compute resources which is a very powerful feature of many application frameworks.

### Example use cases

**Non-blocking workloads**

You might need to perform some complex, slow-running logic in a Payload [Hook](/docs/hooks/overview) but you don't want that hook to "block" or slow down the response returned from the Payload API. Instead of running this logic directly in a hook, which would block your API response from returning until the expensive work is completed, you can queue a new Job and let it run at a later date.

Examples:

- Create vector embeddings from your documents, and keep them in sync as your documents change
- Send data to a third-party API on document change
- Trigger emails based on customer actions

**Scheduled actions**

If you need to schedule an action to be run or processed at a certain date in the future, you can queue a job with the `waitUntil` property set. This will make it so the job is not "picked up" until that `waitUntil` date has passed.

Examples:

- Process scheduled posts, where the scheduled date is at a time set in the future
- Unpublish posts at a given time
- Send a reminder email to a customer after X days of signing up for a trial

**Periodic sync or similar scheduled action**

Some applications may need to perform a regularly scheduled operation of some type. Jobs are perfect for this because you can execute their logic using `cron`, scheduled nightly, every twelve hours, or some similar time period.

Examples:

- You'd like to send emails to all customers on a regular, scheduled basis
- Periodically trigger a rebuild of your frontend at night
- Sync resources to or from a third-party API during non-peak times

**Offloading complex operations**

You may run into the need to perform computationally expensive functions which might slow down your main Payload API server(s). The Jobs Queue allows you to offload these tasks to a separate compute resource rather than slowing down the server(s) that run your Payload APIs. With Payload Task definitions, you can even keep large dependencies out of your main Next.js bundle by dynamically importing them only when they are used. This keeps your Next.js + Payload compilation fast and ensures large dependencies do not get bundled into your Payload production build.

Examples:

- You need to create (and then keep in sync) vector embeddings of your documents as they change, but you use an open source model to generate embeddings
- You have a PDF generator that needs to dynamically build and send PDF versions of documents to customers
- You need to use a headless browser to perform some type of logic
- You need to perform a series of actions, each of which depends on a prior action and should be run in as "durable" of a fashion as possible

### How it works

There are a few concepts that you should become familiarized with before using Payload's Jobs Queue. We recommend learning what each of these does in order to fully understand how to leverage the power of Payload's Jobs Queue.

1. [Tasks](/docs/jobs-queue/tasks)
1. [Workflows](/docs/jobs-queue/workflows)
1. [Jobs](/docs/jobs-queue/jobs)
1. [Queues](/docs/jobs-queue/queues)

All of these pieces work together in order to allow you to offload long-running, expensive, or future scheduled work from your main APIs.

Here's a quick overview:

- A Task is a specific function that performs business logic
- Workflows are groupings of specific tasks which should be run in-order, and can be retried from a specific point of failure
- A Job is an instance of a single task or workflow which will be executed
- A Queue is a way to segment your jobs into different "groups" - for example, some to run nightly, and others to run every 10 minutes

### Visualizing Jobs in the Admin UI

By default, the internal `payload-jobs` collection is hidden from the Payload Admin Panel. To make this collection visible for debugging or inspection purposes, you can override its configuration using `jobsCollectionOverrides`.

```ts
import { buildConfig } from 'payload'

export default buildConfig({
  // ... other config
  jobs: {
    // ... other job settings
    jobsCollectionOverrides: ({ defaultJobsCollection }) => {
      if (!defaultJobsCollection.admin) {
        defaultJobsCollection.admin = {}
      }

      defaultJobsCollection.admin.hidden = false
      return defaultJobsCollection
    },
  },
})
```

---

## 📚 Extended Documentation

<Banner type="success">
**Note**: The documentation below has been automatically generated based on source code analysis and contains more detailed information than the original documentation above.
</Banner>

## Detailed Overview

The PayloadCMS Jobs Queue Core Module provides a comprehensive, enterprise-grade job processing system that enables background task execution, workflow orchestration, and scheduled processing. This internal system creates and manages multiple specialized collections and globals to handle task definitions, job execution, retry logic, error handling, and scheduling infrastructure.

The module implements sophisticated features including multi-queue job processing, automatic retry mechanisms with exponential backoff, workflow orchestration with dependency management, scheduled job execution with cron support, comprehensive error handling and recovery, job statistics and monitoring, and seamless integration with PayloadCMS collections and authentication systems.

Key benefits include non-blocking API responses through background processing, robust error handling with configurable retry policies, scalable architecture supporting multiple worker processes, comprehensive scheduling system for future and recurring tasks, workflow orchestration for complex multi-step operations, and detailed logging and monitoring capabilities for production debugging.

<Banner type="info">
The package is open-source. [View source code](https://github.com/payloadcms/payload/tree/main/packages/payload/src/queues). Need help? [Community Help](https://payloadcms.com/community-help).
</Banner>

## System Requirements

- **PayloadCMS**: ^3.0.0
- **Node.js**: >=18.0.0
- **Database**: MongoDB, PostgreSQL, or SQLite
- **Authentication**: Required for job access control

## Installation

The jobs queue module is included automatically with PayloadCMS core and doesn't require separate installation:

```bash
# npm
npm install payload

# yarn  
yarn add payload

# pnpm
pnpm add payload
```

## Quick Start

Configure basic job processing with tasks and workflows:

```typescript
import type { Config } from 'payload'

export const config: Config = {
  // ... other config
  jobs: {
    // Define tasks for individual operations
    tasks: [
      {
        slug: 'send-email',
        handler: async ({ input, job, req }) => {
          // Send email logic here
          console.log('Sending email to:', input.email)
          await sendEmail(input.email, input.subject, input.body)
          
          return {
            output: {
              emailSent: true,
              sentAt: new Date().toISOString()
            }
          }
        },
        inputSchema: [
          { name: 'email', type: 'text', required: true },
          { name: 'subject', type: 'text', required: true },
          { name: 'body', type: 'richText', required: true }
        ],
        outputSchema: [
          { name: 'emailSent', type: 'checkbox' },
          { name: 'sentAt', type: 'date' }
        ]
      }
    ],
    
    // Define workflows for multi-step operations
    workflows: [
      {
        slug: 'user-onboarding',
        handler: async ({ input, job, tasks }) => {
          // Step 1: Send welcome email
          await tasks['send-email']('welcome-email', {
            input: {
              email: input.userEmail,
              subject: 'Welcome!',
              body: 'Welcome to our platform!'
            }
          })
          
          // Step 2: Set up user preferences
          await tasks['setup-preferences']('setup', {
            input: { userId: input.userId }
          })
        },
        inputSchema: [
          { name: 'userId', type: 'text', required: true },
          { name: 'userEmail', type: 'email', required: true }
        ]
      }
    ],
    
    // Configure automatic job processing
    autoRun: [
      {
        queue: 'default',
        cron: '* * * * *', // Every minute
        limit: 10
      }
    ]
  }
}
```

### Queue and Run Jobs

```typescript
// Queue a single task
const job = await payload.jobs.queue({
  task: 'send-email',
  input: {
    email: 'user@example.com',
    subject: 'Hello!',
    body: 'This is a test email'
  }
})

// Queue a workflow
const workflowJob = await payload.jobs.queue({
  workflow: 'user-onboarding',
  input: {
    userId: '123',
    userEmail: 'user@example.com'
  }
})

// Schedule a job for later
const scheduledJob = await payload.jobs.queue({
  task: 'send-email',
  input: { /* ... */ },
  waitUntil: new Date(Date.now() + 24 * 60 * 60 * 1000) // 24 hours from now
})

// Run jobs manually
const result = await payload.jobs.run({
  queue: 'default',
  limit: 5
})
```

## Detailed Configuration

### Main Configuration Options

#### `jobs.tasks`

- **Type**: `TaskConfig[]`
- **Default**: `[]`
- **Required**: No

Define individual task operations that can be executed as standalone jobs or as part of workflows.

```typescript
tasks: [
  {
    slug: 'process-image',
    handler: async ({ input, job, req }) => {
      const processedImage = await processImage(input.imageId)
      return {
        output: {
          processedUrl: processedImage.url,
          size: processedImage.size
        }
      }
    },
    inputSchema: [
      { name: 'imageId', type: 'text', required: true },
      { name: 'quality', type: 'number', defaultValue: 80 }
    ],
    outputSchema: [
      { name: 'processedUrl', type: 'text' },
      { name: 'size', type: 'number' }
    ],
    retries: {
      attempts: 3,
      backoff: {
        type: 'exponential',
        delay: 1000
      }
    },
    schedule: [
      {
        cron: '0 2 * * *', // Daily at 2 AM
        queue: 'maintenance'
      }
    ]
  }
]
```

#### `jobs.workflows`

- **Type**: `WorkflowConfig[]`
- **Default**: `[]`
- **Required**: No

Define multi-step workflows that orchestrate multiple tasks with dependency management and error recovery.

```typescript
workflows: [
  {
    slug: 'content-publishing',
    handler: async ({ input, job, tasks, inlineTask }) => {
      // Step 1: Validate content
      const validation = await inlineTask('validate-content', {
        input: { contentId: input.contentId },
        task: async ({ input }) => {
          const isValid = await validateContent(input.contentId)
          return {
            output: { isValid },
            state: isValid ? 'succeeded' : 'failed'
          }
        }
      })
      
      if (!validation.isValid) {
        throw new Error('Content validation failed')
      }
      
      // Step 2: Generate thumbnails
      await tasks['generate-thumbnails']('thumbnails', {
        input: { contentId: input.contentId }
      })
      
      // Step 3: Publish content
      await tasks['publish-content']('publish', {
        input: { contentId: input.contentId }
      })
    },
    retries: 2,
    queue: 'publishing'
  }
]
```

#### `jobs.autoRun`

- **Type**: `AutorunCronConfig[] | ((payload: Payload) => AutorunCronConfig[])`
- **Default**: `[]`
- **Required**: No

Configure automatic job processing on specified schedules.

```typescript
autoRun: [
  {
    queue: 'default',
    cron: '*/5 * * * *', // Every 5 minutes
    limit: 20,
    silent: false
  },
  {
    queue: 'priority',
    cron: '* * * * *', // Every minute
    limit: 5,
    allQueues: false
  }
]
```

### Configuration Schema

```typescript
// Main jobs configuration
interface JobsConfig {
  tasks?: TaskConfig[]
  workflows?: WorkflowConfig[]
  autoRun?: AutorunCronConfig[] | ((payload: Payload) => AutorunCronConfig[])
  access?: {
    run?: RunJobAccess
  }
  depth?: number
  deleteJobOnComplete?: boolean
  processingOrder?: Sort | ProcessingOrderConfig
  runHooks?: boolean
  shouldAutoRun?: (payload: Payload) => boolean | Promise<boolean>
  jobsCollectionOverrides?: (args: { defaultJobsCollection: CollectionConfig }) => CollectionConfig
}

// Task configuration
interface TaskConfig {
  slug: string
  handler: string | TaskHandler
  inputSchema?: Field[]
  outputSchema?: Field[]
  label?: string
  retries?: number | RetryConfig
  schedule?: ScheduleConfig[]
  onSuccess?: () => void | Promise<void>
  onFail?: () => void | Promise<void>
}

// Workflow configuration
interface WorkflowConfig {
  slug: string
  handler: string | WorkflowHandler | WorkflowJSON
  inputSchema?: Field[]
  label?: string
  queue?: string
  retries?: number | RetryConfig
  schedule?: ScheduleConfig[]
}

// Job structure
interface Job {
  id: string | number
  input: object
  queue: string
  taskSlug?: string
  workflowSlug?: string
  waitUntil?: string
  processing: boolean
  completedAt?: string
  hasError: boolean
  error?: object
  totalTried: number
  log: JobLog[]
  taskStatus: JobTaskStatus
  meta?: object
}
```

## Usage Guides

### Creating Advanced Task Handlers

Implement sophisticated task handlers with comprehensive error handling and resource management:

```typescript
import type { TaskConfig } from 'payload'

export const advancedImageProcessor: TaskConfig = {
  slug: 'advanced-image-process',
  handler: async ({ input, job, req, tasks, inlineTask }) => {
    const { imageId, operations, options } = input
    
    try {
      // Step 1: Download image with retry logic
      const imageBuffer = await inlineTask('download-image', {
        input: { imageId },
        retries: 3,
        task: async ({ input }) => {
          const response = await fetch(input.imageId)
          if (!response.ok) {
            return { state: 'failed', errorMessage: 'Failed to download image' }
          }
          
          const buffer = await response.arrayBuffer()
          return {
            output: { buffer: Array.from(new Uint8Array(buffer)) },
            state: 'succeeded'
          }
        }
      })
      
      // Step 2: Process each operation
      let processedBuffer = Buffer.from(imageBuffer.buffer)
      
      for (const operation of operations) {
        processedBuffer = await processImageOperation(processedBuffer, operation)
      }
      
      // Step 3: Upload processed image
      const uploadResult = await tasks['upload-image']('upload', {
        input: {
          buffer: Array.from(processedBuffer),
          filename: `processed_${imageId}`,
          mimeType: options.outputFormat || 'image/jpeg'
        }
      })
      
      // Step 4: Update database
      await req.payload.update({
        collection: 'images',
        id: imageId,
        data: {
          processedUrl: uploadResult.url,
          processedAt: new Date().toISOString(),
          operations: operations
        }
      })
      
      return {
        output: {
          processedUrl: uploadResult.url,
          originalSize: imageBuffer.buffer.length,
          processedSize: processedBuffer.length,
          operations: operations.length
        }
      }
    } catch (error) {
      // Log detailed error information
      req.payload.logger.error({
        msg: 'Image processing failed',
        imageId,
        operations,
        error: error.message
      })
      
      return {
        state: 'failed',
        errorMessage: `Image processing failed: ${error.message}`
      }
    }
  },
  
  inputSchema: [
    { name: 'imageId', type: 'text', required: true },
    {
      name: 'operations',
      type: 'array',
      fields: [
        {
          name: 'type',
          type: 'select',
          options: ['resize', 'crop', 'rotate', 'filter']
        },
        { name: 'params', type: 'json' }
      ]
    },
    {
      name: 'options',
      type: 'group',
      fields: [
        { name: 'outputFormat', type: 'text' },
        { name: 'quality', type: 'number', defaultValue: 80 }
      ]
    }
  ],
  
  outputSchema: [
    { name: 'processedUrl', type: 'text' },
    { name: 'originalSize', type: 'number' },
    { name: 'processedSize', type: 'number' },
    { name: 'operations', type: 'number' }
  ],
  
  retries: {
    attempts: 3,
    backoff: {
      type: 'exponential',
      delay: 2000
    },
    shouldRestore: async ({ input, taskStatus }) => {
      // Only restore if processing took less than 5 minutes
      const processingTime = new Date().getTime() - new Date(taskStatus.input.startTime || 0).getTime()
      return processingTime < 5 * 60 * 1000
    }
  },
  
  onSuccess: async () => {
    console.log('Image processing completed successfully')
  },
  
  onFail: async () => {
    console.log('Image processing failed after all retries')
  }
}
```

### Complex Workflow Orchestration

Create sophisticated workflows with conditional logic and parallel processing:

```typescript
export const ecommerceOrderWorkflow: WorkflowConfig = {
  slug: 'process-order',
  handler: async ({ input, job, tasks, inlineTask }) => {
    const { orderId, customerData, items } = input
    
    // Step 1: Validate order data in parallel
    const [inventoryCheck, paymentValidation, customerValidation] = await Promise.all([
      inlineTask('check-inventory', {
        input: { items },
        task: async ({ input }) => {
          const availability = await checkInventoryAvailability(input.items)
          return {
            output: { available: availability.allAvailable, issues: availability.issues },
            state: availability.allAvailable ? 'succeeded' : 'failed'
          }
        }
      }),
      
      tasks['validate-payment']('payment-check', {
        input: { paymentMethod: customerData.paymentMethod, amount: input.totalAmount }
      }),
      
      tasks['validate-customer']('customer-check', {
        input: { customerId: customerData.id }
      })
    ])
    
    if (!inventoryCheck.available) {
      throw new Error(`Inventory unavailable: ${inventoryCheck.issues.join(', ')}`)
    }
    
    // Step 2: Process payment
    const paymentResult = await tasks['process-payment']('payment', {
      input: {
        orderId,
        amount: input.totalAmount,
        paymentMethod: customerData.paymentMethod
      },
      retries: 2 // Critical step with retries
    })
    
    // Step 3: Update inventory (reduce stock)
    await tasks['update-inventory']('inventory-update', {
      input: { items, operation: 'reduce' }
    })
    
    // Step 4: Create shipment record
    const shipmentResult = await tasks['create-shipment']('shipment', {
      input: {
        orderId,
        items,
        shippingAddress: customerData.shippingAddress
      }
    })
    
    // Step 5: Send confirmation emails in parallel (non-blocking)
    const emailPromises = [
      tasks['send-email']('customer-confirmation', {
        input: {
          to: customerData.email,
          template: 'order-confirmation',
          data: { orderId, items, trackingNumber: shipmentResult.trackingNumber }
        }
      }),
      
      tasks['send-email']('admin-notification', {
        input: {
          to: 'admin@store.com',
          template: 'new-order',
          data: { orderId, customerData, totalAmount: input.totalAmount }
        }
      })
    ]
    
    // Don't wait for emails to complete - they'll retry if needed
    Promise.all(emailPromises).catch(error => {
      job.logger?.error('Email sending failed:', error)
    })
    
    // Step 6: Schedule follow-up tasks
    await req.payload.jobs.queue({
      task: 'send-shipping-updates',
      input: { orderId, trackingNumber: shipmentResult.trackingNumber },
      waitUntil: new Date(Date.now() + 24 * 60 * 60 * 1000) // 24 hours later
    })
    
    // Update order status
    await req.payload.update({
      collection: 'orders',
      id: orderId,
      data: {
        status: 'processed',
        paymentId: paymentResult.transactionId,
        trackingNumber: shipmentResult.trackingNumber,
        processedAt: new Date().toISOString()
      }
    })
  },
  
  inputSchema: [
    { name: 'orderId', type: 'text', required: true },
    { name: 'totalAmount', type: 'number', required: true },
    {
      name: 'customerData',
      type: 'group',
      fields: [
        { name: 'id', type: 'text' },
        { name: 'email', type: 'email' },
        { name: 'paymentMethod', type: 'text' },
        { name: 'shippingAddress', type: 'group', fields: [/* address fields */] }
      ]
    },
    {
      name: 'items',
      type: 'array',
      fields: [
        { name: 'productId', type: 'text' },
        { name: 'quantity', type: 'number' },
        { name: 'price', type: 'number' }
      ]
    }
  ],
  
  retries: {
    attempts: 2,
    backoff: { type: 'fixed', delay: 5000 }
  },
  
  queue: 'order-processing'
}
```

### Advanced Patterns

#### JSON Workflow Definition

Use JSON workflow definitions for dynamic workflow creation:

```typescript
export const dynamicApprovalWorkflow: WorkflowConfig = {
  slug: 'dynamic-approval',
  handler: [
    {
      id: 'initial-review',
      task: 'content-review',
      input: ({ job }) => ({
        contentId: job.input.contentId,
        reviewType: 'initial'
      }),
      condition: ({ job }) => job.input.requiresReview,
      retries: 1
    },
    {
      id: 'manager-approval',
      task: 'approval-request', 
      input: ({ job }) => ({
        contentId: job.input.contentId,
        approverRole: 'manager',
        previousReviewId: 'initial-review'
      }),
      condition: ({ job }) => {
        const reviewResult = job.taskStatus['content-review']?.['initial-review']
        return reviewResult?.complete && reviewResult.output.requiresManagerApproval
      }
    },
    {
      id: 'publish-content',
      task: 'publish-content',
      input: ({ job }) => ({
        contentId: job.input.contentId
      }),
      completesJob: true,
      condition: ({ job }) => {
        const approvalResult = job.taskStatus['approval-request']?.['manager-approval']
        return approvalResult?.complete && approvalResult.output.approved
      }
    }
  ],
  
  inputSchema: [
    { name: 'contentId', type: 'text', required: true },
    { name: 'requiresReview', type: 'checkbox', defaultValue: true }
  ]
}
```

#### Custom Scheduling Logic

Implement sophisticated scheduling with custom hooks:

```typescript
export const smartSchedulingWorkflow: WorkflowConfig = {
  slug: 'smart-backup',
  schedule: [
    {
      cron: '0 2 * * *', // Daily at 2 AM
      queue: 'maintenance',
      hooks: {
        beforeSchedule: async ({ queueable, jobStats, req }) => {
          // Check system load before scheduling
          const systemLoad = await getSystemLoad()
          const recentBackups = await getRecentBackupCount()
          
          if (systemLoad > 0.8) {
            req.payload.logger.info('Skipping backup due to high system load')
            return { shouldSchedule: false }
          }
          
          if (recentBackups > 0) {
            req.payload.logger.info('Backup already completed today')
            return { shouldSchedule: false }
          }
          
          // Determine backup scope based on data changes
          const dataChanged = await checkDataChanges()
          const backupType = dataChanged.significant ? 'full' : 'incremental'
          
          return {
            shouldSchedule: true,
            input: {
              backupType,
              includeUploads: dataChanged.uploadsChanged,
              retentionDays: backupType === 'full' ? 30 : 7
            },
            waitUntil: new Date(Date.now() + (systemLoad * 3600000)) // Delay based on load
          }
        },
        
        afterSchedule: async ({ status, job, jobStats, req }) => {
          if (status === 'success' && job) {
            // Update backup statistics
            await req.payload.update({
              collection: 'system-stats',
              id: 'backup-stats',
              data: {
                lastScheduled: new Date().toISOString(),
                nextBackupType: job.input.backupType,
                scheduledJobs: (jobStats.scheduledJobs || 0) + 1
              }
            })
          }
        }
      }
    }
  ]
}
```

## API Reference

### Constants

#### `jobsCollectionSlug`

- **Value**: `'payload-jobs'`
- **Description**: The slug of the internal collection used to store job records

#### `jobStatsGlobalSlug`

- **Value**: `'payload-jobs-stats'`  
- **Description**: The slug of the internal global used to store job statistics

### Functions

#### `getDefaultJobsCollection(jobsConfig: SanitizedJobsConfig)`

Creates the internal collection configuration for job storage and management.

**Parameters:**
| Parameter | Type | Description |
|-----------|------|-------------|
| `jobsConfig` | `SanitizedJobsConfig` | The sanitized jobs configuration |

**Returns:** `CollectionConfig`

#### `getJobStatsGlobal(config: Config)`

Creates the internal global configuration for job statistics tracking.

**Parameters:**
| Parameter | Type | Description |
|-----------|------|-------------|
| `config` | `Config` | The main PayloadCMS configuration object |

**Returns:** `GlobalConfig`

#### `runJobs(args: RunJobsArgs)`

Main function for processing queued jobs with comprehensive options.

**Parameters:**
| Parameter | Type | Description |
|-----------|------|-------------|
| `args.queue` | `string` | Queue name to process (default: 'default') |
| `args.limit` | `number` | Maximum jobs to process (default: 10) |
| `args.allQueues` | `boolean` | Process all queues (default: false) |
| `args.sequential` | `boolean` | Process jobs sequentially (default: false) |
| `args.silent` | `RunJobsSilent` | Suppress logging output |
| `args.processingOrder` | `Sort` | Job processing order |
| `args.where` | `Where` | Additional query constraints |

**Returns:** `Promise<RunJobsResult>`

#### `handleSchedules(args: HandleSchedulesArgs)`

Processes scheduled job creation based on cron configurations.

**Parameters:**
| Parameter | Type | Description |
|-----------|------|-------------|
| `args.queue` | `string` | Queue to schedule jobs for |
| `args.allQueues` | `boolean` | Schedule for all queues |
| `args.req` | `PayloadRequest` | Request object |

**Returns:** `Promise<HandleSchedulesResult>`

### Local API Methods

#### `payload.jobs.queue(args)`

Queue a new job for execution.

```typescript
const job = await payload.jobs.queue({
  task: 'send-email',
  input: { email: 'user@example.com' },
  queue: 'notifications',
  waitUntil: new Date(Date.now() + 3600000) // 1 hour delay
})
```

#### `payload.jobs.run(args)`

Manually process queued jobs.

```typescript
const result = await payload.jobs.run({
  queue: 'default',
  limit: 5,
  sequential: true
})
```

#### `payload.jobs.cancel(args)`

Cancel queued jobs matching criteria.

```typescript
await payload.jobs.cancel({
  where: { queue: { equals: 'slow-queue' } }
})
```

### TypeScript Types

```typescript
// Core job types
interface Job<TWorkflowSlugOrInput = false> {
  id: string | number
  input: TWorkflowSlugOrInput extends keyof TypedJobs['workflows']
    ? TypedJobs['workflows'][TWorkflowSlugOrInput]['input']
    : object
  queue: string
  taskSlug?: string
  workflowSlug?: string
  waitUntil?: string
  processing: boolean
  completedAt?: string
  hasError: boolean
  error?: object
  totalTried: number
  log: JobLog[]
  taskStatus: JobTaskStatus
  meta?: object
}

// Task configuration
interface TaskConfig<TTaskSlugOrInputOutput = string> {
  slug: string
  handler: string | TaskHandler<TTaskSlugOrInputOutput>
  inputSchema?: Field[]
  outputSchema?: Field[]
  interfaceName?: string
  label?: string
  retries?: number | RetryConfig
  schedule?: ScheduleConfig[]
  onSuccess?: () => void | Promise<void>
  onFail?: () => void | Promise<void>
}

// Workflow configuration
interface WorkflowConfig<TWorkflowSlugOrInput = false> {
  slug: string
  handler: string | WorkflowHandler<TWorkflowSlugOrInput> | WorkflowJSON<TWorkflowSlugOrInput>
  inputSchema?: Field[]
  interfaceName?: string
  label?: string
  queue?: string
  retries?: number | RetryConfig
  schedule?: ScheduleConfig[]
}

// Job execution results
interface RunJobsResult {
  jobStatus?: Record<string, RunJobResult>
  noJobsRemaining?: boolean
  remainingJobsFromQueried: number
}
```

## Integrations

### PayloadCMS Collections

The jobs system integrates deeply with PayloadCMS:

- **Internal Collections**: Automatically creates `payload-jobs` collection for job storage
- **Collection Hooks**: Jobs can be triggered from collection hooks for automated processing
- **Authentication**: Respects PayloadCMS authentication and access control systems
- **Database Operations**: Seamlessly works with PayloadCMS database adapters

### Database Integration

The system creates and manages specialized collections:

- **Jobs Collection**: Stores job records with comprehensive metadata
- **Stats Global**: Tracks scheduling statistics and system metrics
- **Optimized Queries**: Uses database-specific optimizations for job processing
- **Transaction Support**: Handles database transactions for job state consistency

### External Systems

Jobs can integrate with external services:

- **HTTP APIs**: Call external REST APIs with retry logic
- **Message Queues**: Integrate with Redis, RabbitMQ, or other queue systems
- **File Storage**: Process files from various storage providers
- **Email Services**: Send emails through SMTP or API-based services

## Troubleshooting

### Common Issues

#### Jobs Not Processing

**Problem:** Jobs are queued but not being processed automatically.

**Solution:**
1. Verify `autoRun` configuration is set up correctly
2. Check that the job runner process is active
3. Ensure database connectivity and permissions

**Example:**
```typescript
// Check autoRun configuration
jobs: {
  autoRun: [
    {
      queue: 'default',
      cron: '* * * * *', // Every minute
      limit: 10
    }
  ],
  
  // Enable debugging
  runHooks: false, // For better performance
  depth: 0 // Minimal depth for faster processing
}
```

#### Task Handler Import Errors

**Problem:** Getting errors when importing task handlers from file paths.

**Solution:**
Use function handlers instead of string paths, or ensure proper build configuration:

**Example:**
```typescript
// ❌ Wrong - string path may fail in production
handler: './tasks/sendEmail.js'

// ✅ Correct - direct function reference
handler: async ({ input, job, req }) => {
  // Task logic here
  return { output: {} }
}
```

#### Job Retry Loops

**Problem:** Jobs getting stuck in infinite retry loops.

**Solution:**
Configure appropriate retry limits and backoff strategies:

**Example:**
```typescript
retries: {
  attempts: 3, // Limit retry attempts
  backoff: {
    type: 'exponential',
    delay: 1000 // Start with 1 second delay
  },
  shouldRestore: async ({ taskStatus, input }) => {
    // Only restore if task completed recently
    const completedAt = new Date(taskStatus.completedAt || 0)
    const now = new Date()
    return (now.getTime() - completedAt.getTime()) < 3600000 // 1 hour
  }
}
```

#### Memory Leaks in Long-Running Jobs

**Problem:** Memory usage increasing during job processing.

**Solution:**
1. Use streaming for large data processing
2. Clean up resources explicitly
3. Process data in chunks

**Example:**
```typescript
handler: async ({ input }) => {
  const results = []
  const chunkSize = 100
  
  for (let i = 0; i < input.items.length; i += chunkSize) {
    const chunk = input.items.slice(i, i + chunkSize)
    const processedChunk = await processChunk(chunk)
    results.push(...processedChunk)
    
    // Force garbage collection between chunks
    if (global.gc) {
      global.gc()
    }
  }
  
  return { output: { processed: results.length } }
}
```

### Debugging

Enable comprehensive debugging for job processing:

```typescript
export const config: Config = {
  jobs: {
    // Enable hooks for debugging (reduces performance)
    runHooks: true,
    depth: 1,
    
    // Custom job collection for debugging
    jobsCollectionOverrides: ({ defaultJobsCollection }) => ({
      ...defaultJobsCollection,
      admin: {
        ...defaultJobsCollection.admin,
        hidden: false, // Show in admin interface
        defaultColumns: ['taskSlug', 'workflowSlug', 'queue', 'processing', 'hasError', 'createdAt']
      }
    }),
    
    // Debug logging
    tasks: [
      {
        slug: 'debug-task',
        handler: async ({ input, job, req }) => {
          req.payload.logger.info('Debug task executed', {
            jobId: job.id,
            input,
            timestamp: new Date().toISOString()
          })
          
          return { output: { debugComplete: true } }
        }
      }
    ]
  }
}
```

Monitor job processing in production:

```typescript
// Create monitoring endpoint
const monitorJobs = async (payload: Payload) => {
  const stats = await payload.db.count({
    collection: 'payload-jobs',
    req: await createLocalReq({}, payload)
  })
  
  const processingJobs = await payload.find({
    collection: 'payload-jobs',
    where: { processing: { equals: true } },
    limit: 100
  })
  
  const failedJobs = await payload.find({
    collection: 'payload-jobs',
    where: { hasError: { equals: true } },
    limit: 10,
    sort: '-updatedAt'
  })
  
  return {
    totalJobs: stats.totalDocs,
    processing: processingJobs.totalDocs,
    recentFailures: failedJobs.docs.map(job => ({
      id: job.id,
      error: job.error,
      task: job.taskSlug || job.workflowSlug,
      failedAt: job.updatedAt
    }))
  }
}
```

## Performance

### Performance Optimization

1. **Queue Segmentation**: Use multiple queues for different priority levels
2. **Batch Processing**: Process related jobs in batches when possible
3. **Connection Pooling**: Optimize database connection usage
4. **Resource Management**: Clean up resources after job completion

```typescript
// Optimized job processing configuration
jobs: {
  processingOrder: {
    default: 'createdAt', // FIFO for fairness
    queues: {
      priority: '-createdAt', // LIFO for priority jobs
      bulk: 'createdAt' // FIFO for bulk operations
    }
  },
  
  deleteJobOnComplete: true, // Clean up completed jobs
  depth: 0, // Minimal depth for performance
  runHooks: false, // Direct database operations
  
  autoRun: [
    {
      queue: 'priority',
      cron: '* * * * *', // Every minute
      limit: 5 // Smaller limit for priority
    },
    {
      queue: 'bulk',
      cron: '*/5 * * * *', // Every 5 minutes
      limit: 50 // Larger batches for bulk operations
    }
  ]
}
```

## Security

### Security Considerations

1. **Access Control**: Implement proper job execution permissions
2. **Input Validation**: Validate all job input data
3. **Resource Limits**: Prevent resource exhaustion attacks
4. **Audit Logging**: Track job execution for security monitoring

```typescript
jobs: {
  access: {
    run: ({ req }) => {
      // Only authenticated users with job execution permission
      return req.user && req.user.roles?.includes('job-runner')
    }
  },
  
  tasks: [
    {
      slug: 'secure-task',
      handler: async ({ input, job, req }) => {
        // Validate input
        if (!input || typeof input !== 'object') {
          throw new Error('Invalid input data')
        }
        
        // Check user permissions
        if (!req.user || !req.user.roles?.includes('task-executor')) {
          throw new Error('Insufficient permissions')
        }
        
        // Sanitize input data
        const sanitizedInput = sanitizeJobInput(input)
        
        // Process with resource limits
        return await processWithLimits(sanitizedInput, {
          timeout: 30000, // 30 second timeout
          memoryLimit: 100 * 1024 * 1024 // 100MB limit
        })
      }
    }
  ]
}
```

## Migration

### Migrating from Previous Versions

When upgrading job configurations:

```typescript
// Migration helper for job configuration changes
const migrateJobConfiguration = (oldConfig: any) => {
  const newConfig = { ...oldConfig }
  
  // Migrate old task format
  if (oldConfig.tasks) {
    newConfig.tasks = oldConfig.tasks.map(task => ({
      ...task,
      // Update handler path format
      handler: task.handler.startsWith('./') 
        ? path.resolve(process.cwd(), task.handler)
        : task.handler,
      
      // Migrate retry configuration
      retries: typeof task.retries === 'number' 
        ? { attempts: task.retries }
        : task.retries
    }))
  }
  
  return newConfig
}
```

## Contributing

Found a bug or have a suggestion? [Open an issue](https://github.com/payloadcms/payload/issues) or submit a Pull Request.

## License

MIT License - see the [LICENSE](https://github.com/payloadcms/payload/blob/main/LICENSE) file for details.