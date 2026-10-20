
# SubscriptionModelUsage

One model\'s plan-covered usage in a window. Cached input is part of `input_tokens` and counts toward the allowance in full; it is broken out only so you can see how much of your input was cache reads.

## Properties

Name | Type
------------ | -------------
`model` | string
`inputTokens` | number
`cachedInputTokens` | number
`outputTokens` | number
`usageFactorMilli` | number
`weightedInputTokens` | number
`weightedOutputTokens` | number

## Example

```typescript
import type { SubscriptionModelUsage } from '@deeprelay/sdk'

// TODO: Update the object below with actual values
const example = {
  "model": null,
  "inputTokens": null,
  "cachedInputTokens": null,
  "outputTokens": null,
  "usageFactorMilli": null,
  "weightedInputTokens": null,
  "weightedOutputTokens": null,
} satisfies SubscriptionModelUsage

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as SubscriptionModelUsage
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


