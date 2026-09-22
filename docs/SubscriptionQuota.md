
# SubscriptionQuota

The plan\'s configured allowances — the denominators of the usage meter. Always present, including for an organization that has not subscribed, where it describes what subscribing would provide.  Token figures are WEIGHTED tokens: every model carries a usage factor, so a model at factor 2 spends two of these per token it serves. 

## Properties

Name | Type
------------ | -------------
`inputTokensMonthly` | number
`outputTokensMonthly` | number
`weeklyTokens` | number
`maxUsageMicroCents` | number
`paygDiscountBp` | number

## Example

```typescript
import type { SubscriptionQuota } from '@deeprelay/sdk'

// TODO: Update the object below with actual values
const example = {
  "inputTokensMonthly": null,
  "outputTokensMonthly": null,
  "weeklyTokens": null,
  "maxUsageMicroCents": null,
  "paygDiscountBp": null,
} satisfies SubscriptionQuota

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as SubscriptionQuota
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


