
# SubscriptionPaygEstimate

What this period\'s plan-covered traffic would have cost on pay-as-you-go, read off the request ledger. `list_micro_cents` is exact: every covered request records its list price with the model\'s cached-input rate honored. `uncached_micro_cents` is the same traffic with every cache read billed at the full input rate (today\'s off-peak rates, so approximate); the gap is the cached-input discount, which the plan allowance does not give (cached input counts in full). The token counts are the raw input and its cached subset over the period. Omitted from `usage` until the period has covered usage.

## Properties

Name | Type
------------ | -------------
`periodStart` | Date
`periodEnd` | Date
`listMicroCents` | number
`uncachedMicroCents` | number
`inputTokens` | number
`cachedInputTokens` | number

## Example

```typescript
import type { SubscriptionPaygEstimate } from '@deeprelay/sdk'

// TODO: Update the object below with actual values
const example = {
  "periodStart": null,
  "periodEnd": null,
  "listMicroCents": null,
  "uncachedMicroCents": null,
  "inputTokens": null,
  "cachedInputTokens": null,
} satisfies SubscriptionPaygEstimate

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as SubscriptionPaygEstimate
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


