
# SubscriptionTier

One plan as the plan catalogue lists it: identity, price and the allowance it buys. Every offered plan covers the same models at the same usage factors — Plus is Base with a larger allowance. 

## Properties

Name | Type
------------ | -------------
`key` | string
`name` | string
`price` | [SubscriptionPrice](SubscriptionPrice.md)
`quota` | [SubscriptionQuota](SubscriptionQuota.md)

## Example

```typescript
import type { SubscriptionTier } from '@deeprelay/sdk'

// TODO: Update the object below with actual values
const example = {
  "key": null,
  "name": null,
  "price": null,
  "quota": null,
} satisfies SubscriptionTier

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as SubscriptionTier
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


