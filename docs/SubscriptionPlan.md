
# SubscriptionPlan

What the organization is — or would be — subscribing to. Always present, including for an organization that never subscribed: it is what a point of purchase renders before sending anyone to pay. 

## Properties

Name | Type
------------ | -------------
`key` | string
`name` | string
`price` | [SubscriptionPrice](SubscriptionPrice.md)

## Example

```typescript
import type { SubscriptionPlan } from '@deeprelay/sdk'

// TODO: Update the object below with actual values
const example = {
  "key": null,
  "name": null,
  "price": null,
} satisfies SubscriptionPlan

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as SubscriptionPlan
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


