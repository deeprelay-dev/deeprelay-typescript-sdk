
# SubscriptionBalancePayment

How the organization\'s balance splits for paying a plan. free_credit_cents + pending_deposit_cents + spendable_cents equals the balance (zero when the balance is negative). 

## Properties

Name | Type
------------ | -------------
`balanceCents` | number
`spendableCents` | number
`freeCreditCents` | number
`pendingDepositCents` | number
`pendingUntil` | Date

## Example

```typescript
import type { SubscriptionBalancePayment } from '@deeprelay/sdk'

// TODO: Update the object below with actual values
const example = {
  "balanceCents": null,
  "spendableCents": null,
  "freeCreditCents": null,
  "pendingDepositCents": null,
  "pendingUntil": null,
} satisfies SubscriptionBalancePayment

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as SubscriptionBalancePayment
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


