
# Batch

The OpenAI batch object plus a `deeprelay` sub-object with the schedule, rate and cost. Timestamps are Unix seconds, null when unset. A paused batch stays `in_progress` with `deeprelay.pause_reason` set.

## Properties

Name | Type
------------ | -------------
`id` | string
`object` | string
`endpoint` | string
`model` | string
`errors` | object
`inputFileId` | string
`completionWindow` | string
`status` | string
`outputFileId` | string
`errorFileId` | string
`createdAt` | number
`inProgressAt` | number
`expiresAt` | number
`finalizingAt` | number
`completedAt` | number
`failedAt` | number
`expiredAt` | number
`cancellingAt` | number
`cancelledAt` | number
`requestCounts` | [BatchRequestCounts](BatchRequestCounts.md)
`usage` | [BatchUsage](BatchUsage.md)
`metadata` | { [key: string]: string; }
`deeprelay` | [BatchDeeprelay](BatchDeeprelay.md)

## Example

```typescript
import type { Batch } from '@deeprelay/sdk'

// TODO: Update the object below with actual values
const example = {
  "id": null,
  "object": null,
  "endpoint": null,
  "model": null,
  "errors": null,
  "inputFileId": null,
  "completionWindow": null,
  "status": null,
  "outputFileId": null,
  "errorFileId": null,
  "createdAt": null,
  "inProgressAt": null,
  "expiresAt": null,
  "finalizingAt": null,
  "completedAt": null,
  "failedAt": null,
  "expiredAt": null,
  "cancellingAt": null,
  "cancelledAt": null,
  "requestCounts": null,
  "usage": null,
  "metadata": null,
  "deeprelay": null,
} satisfies Batch

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as Batch
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


