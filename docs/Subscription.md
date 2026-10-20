
# Subscription

The organization\'s subscription: entitlement, billing period, the plan it is on with that plan\'s configured quota, consumption against it, and the plans this deployment offers. The console and this endpoint assemble it from the same source, so the two surfaces cannot report different numbers. 

## Properties

Name | Type
------------ | -------------
`subscribed` | boolean
`status` | string
`cancelAtPeriodEnd` | boolean
`currentPeriodStart` | Date
`currentPeriodEnd` | Date
`plan` | [SubscriptionPlan](SubscriptionPlan.md)
`quota` | [SubscriptionQuota](SubscriptionQuota.md)
`usage` | [SubscriptionUsage](SubscriptionUsage.md)
`plans` | [Array&lt;SubscriptionTier&gt;](SubscriptionTier.md)

## Example

```typescript
import type { Subscription } from '@deeprelay/sdk'

// TODO: Update the object below with actual values
const example = {
  "subscribed": null,
  "status": null,
  "cancelAtPeriodEnd": null,
  "currentPeriodStart": null,
  "currentPeriodEnd": null,
  "plan": null,
  "quota": null,
  "usage": null,
  "plans": null,
} satisfies Subscription

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as Subscription
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


