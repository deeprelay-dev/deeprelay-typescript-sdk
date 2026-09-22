
# Balance

The organization\'s credit balance with its auto-pay configuration and live burn rate. Mirrors the dashboard\'s balance contract field for field. No payment-instrument detail appears here — saved cards live behind separate admin-only routes. 

## Properties

Name | Type
------------ | -------------
`balanceCents` | number
`balanceDollars` | number
`autoPayEnabled` | boolean
`autoPayThresholdCents` | number
`autoPayAmountCents` | number
`burnCentsPerHour` | number

## Example

```typescript
import type { Balance } from '@deeprelay/sdk'

// TODO: Update the object below with actual values
const example = {
  "balanceCents": null,
  "balanceDollars": null,
  "autoPayEnabled": null,
  "autoPayThresholdCents": null,
  "autoPayAmountCents": null,
  "burnCentsPerHour": null,
} satisfies Balance

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as Balance
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


