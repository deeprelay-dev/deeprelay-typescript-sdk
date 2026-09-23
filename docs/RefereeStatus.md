
# RefereeStatus

Present only when the organization signed up through someone else\'s invite link: where that referral sits and how far the organization is from unlocking its own reward. 

## Properties

Name | Type
------------ | -------------
`status` | string
`spentCents` | number
`qualifySpendCents` | number
`rewardCents` | number
`qualifiedAt` | Date
`holdUntil` | Date
`settledAt` | Date

## Example

```typescript
import type { RefereeStatus } from '@deeprelay/sdk'

// TODO: Update the object below with actual values
const example = {
  "status": null,
  "spentCents": null,
  "qualifySpendCents": null,
  "rewardCents": null,
  "qualifiedAt": null,
  "holdUntil": null,
  "settledAt": null,
} satisfies RefereeStatus

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as RefereeStatus
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


