
# SubscriptionPrice

The plan\'s recurring charge, read live from the billing provider — the single source of truth, never a number embedded in code.  ABSENT means \"price unavailable right now\" (billing unconfigured, or the provider could not be reached). It NEVER means free. Render the plan without a figure rather than substituting one; the hosted checkout page always shows the real amount. 

## Properties

Name | Type
------------ | -------------
`amountCents` | number
`currency` | string
`interval` | string
`intervalCount` | number

## Example

```typescript
import type { SubscriptionPrice } from '@deeprelay/sdk'

// TODO: Update the object below with actual values
const example = {
  "amountCents": null,
  "currency": null,
  "interval": null,
  "intervalCount": null,
} satisfies SubscriptionPrice

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as SubscriptionPrice
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


