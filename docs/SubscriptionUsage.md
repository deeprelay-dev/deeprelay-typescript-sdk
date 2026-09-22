
# SubscriptionUsage

Consumption against the quota, from the same factor-weighted read the request-time gate evaluates — so this meter and enforcement cannot disagree.  Present only for an entitled subscription whose meter could be read. Its absence is never a statement that nothing was used. 

## Properties

Name | Type
------------ | -------------
`periodStart` | Date
`periodEnd` | Date
`weightedInputTokens` | number
`weightedOutputTokens` | number
`weeklyWeightedTokens` | number
`costMicroCents` | number

## Example

```typescript
import type { SubscriptionUsage } from '@deeprelay/sdk'

// TODO: Update the object below with actual values
const example = {
  "periodStart": null,
  "periodEnd": null,
  "weightedInputTokens": null,
  "weightedOutputTokens": null,
  "weeklyWeightedTokens": null,
  "costMicroCents": null,
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


