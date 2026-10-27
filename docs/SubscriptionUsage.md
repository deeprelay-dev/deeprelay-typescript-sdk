
# SubscriptionUsage

Consumption against the quota, from the same factor-weighted read the request-time gate evaluates — so this meter and enforcement cannot disagree.  Present only for an entitled subscription whose meter could be read. Its absence is never a statement that nothing was used. 

## Properties

Name | Type
------------ | -------------
`periodStart` | Date
`periodEnd` | Date
`weightedInputTokens` | number
`weightedOutputTokens` | number
`weeklyWeightedInputTokens` | number
`weeklyWeightedOutputTokens` | number
`costMicroCents` | number
`searches` | number
`recentPaygCalls24h` | number
`byModel` | [Array&lt;SubscriptionModelUsage&gt;](SubscriptionModelUsage.md)
`weeklyByModel` | [Array&lt;SubscriptionModelUsage&gt;](SubscriptionModelUsage.md)

## Example

```typescript
import type { SubscriptionUsage } from '@deeprelay/sdk'

// TODO: Update the object below with actual values
const example = {
  "periodStart": null,
  "periodEnd": null,
  "weightedInputTokens": null,
  "weightedOutputTokens": null,
  "weeklyWeightedInputTokens": null,
  "weeklyWeightedOutputTokens": null,
  "costMicroCents": null,
  "searches": null,
  "recentPaygCalls24h": null,
  "byModel": null,
  "weeklyByModel": null,
} satisfies SubscriptionUsage

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as SubscriptionUsage
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


