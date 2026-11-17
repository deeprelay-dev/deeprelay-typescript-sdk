
# BatchDeeprelay

When the batch runs, at what rate, and for how much. Money is in micro-cents (1e-6 cent); timestamps are Unix seconds.

## Properties

Name | Type
------------ | -------------
`scheduledFor` | number
`currentWindow` | [BatchDeeprelayCurrentWindow](BatchDeeprelayCurrentWindow.md)
`nextWindowAt` | number
`estimatedCompletionAt` | number
`expiresAt` | number
`rateTier` | string
`batchPrice` | [BatchDeeprelayBatchPrice](BatchDeeprelayBatchPrice.md)
`estimatedCost` | [BatchMoney](BatchMoney.md)
`estimatedTokens` | [BatchDeeprelayEstimatedTokens](BatchDeeprelayEstimatedTokens.md)
`cost` | [BatchMoney](BatchMoney.md)
`pauseReason` | string
`windowsRanIn` | Array&lt;number&gt;
`requestCounts` | [BatchDeeprelayRequestCounts](BatchDeeprelayRequestCounts.md)
`limits` | [BatchLimits](BatchLimits.md)

## Example

```typescript
import type { BatchDeeprelay } from '@deeprelay/sdk'

// TODO: Update the object below with actual values
const example = {
  "scheduledFor": null,
  "currentWindow": null,
  "nextWindowAt": null,
  "estimatedCompletionAt": null,
  "expiresAt": null,
  "rateTier": null,
  "batchPrice": null,
  "estimatedCost": null,
  "estimatedTokens": null,
  "cost": null,
  "pauseReason": null,
  "windowsRanIn": null,
  "requestCounts": null,
  "limits": null,
} satisfies BatchDeeprelay

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as BatchDeeprelay
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


