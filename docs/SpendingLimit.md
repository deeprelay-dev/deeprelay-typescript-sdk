
# SpendingLimit


## Properties

Name | Type
------------ | -------------
`monthlyLimitCents` | number
`monthlyLimitDollars` | number
`currentMonthSpendCents` | number
`currentMonthSpendDollars` | number
`percentUsed` | number
`billingCycleStart` | Date
`enforcement` | string
`autoTerminateHours` | number
`dailyLimitCents` | number
`dailyLimitDollars` | number
`currentDaySpendCents` | number

## Example

```typescript
import type { SpendingLimit } from '@deeprelay/sdk'

// TODO: Update the object below with actual values
const example = {
  "monthlyLimitCents": null,
  "monthlyLimitDollars": null,
  "currentMonthSpendCents": null,
  "currentMonthSpendDollars": null,
  "percentUsed": null,
  "billingCycleStart": null,
  "enforcement": null,
  "autoTerminateHours": null,
  "dailyLimitCents": null,
  "dailyLimitDollars": null,
  "currentDaySpendCents": null,
} satisfies SpendingLimit

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as SpendingLimit
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


