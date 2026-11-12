
# ModelBatchPricing

`pricing.batch`: what a Batch API line for this model bills at. Present on chat models while the Batch API is enabled.

## Properties

Name | Type
------------ | -------------
`eligible` | boolean
`rateTier` | string
`inputPer1mTokensMicrocents` | number
`cachedInputPer1mTokensMicrocents` | number
`outputPer1mTokensMicrocents` | number
`scheduleUrl` | string

## Example

```typescript
import type { ModelBatchPricing } from '@deeprelay/sdk'

// TODO: Update the object below with actual values
const example = {
  "eligible": null,
  "rateTier": null,
  "inputPer1mTokensMicrocents": null,
  "cachedInputPer1mTokensMicrocents": null,
  "outputPer1mTokensMicrocents": null,
  "scheduleUrl": null,
} satisfies ModelBatchPricing

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as ModelBatchPricing
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


