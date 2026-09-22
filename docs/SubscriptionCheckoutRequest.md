
# SubscriptionCheckoutRequest

Optional overrides for a checkout mint. Every field has a deployment default, so an empty body is the normal call. 

## Properties

Name | Type
------------ | -------------
`successUrl` | string
`cancelUrl` | string
`planKey` | string

## Example

```typescript
import type { SubscriptionCheckoutRequest } from '@deeprelay/sdk'

// TODO: Update the object below with actual values
const example = {
  "successUrl": null,
  "cancelUrl": null,
  "planKey": null,
} satisfies SubscriptionCheckoutRequest

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as SubscriptionCheckoutRequest
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


