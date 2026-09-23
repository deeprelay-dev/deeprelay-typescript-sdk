
# Referral

The organization\'s referral-program view: its invite link, the program terms, its referrer stats, and (only when it was itself referred) its referee progress. Amounts are USD cents. 

## Properties

Name | Type
------------ | -------------
`code` | string
`inviteUrl` | string
`pending` | number
`qualified` | number
`settled` | number
`earnedCents` | number
`rewardCents` | number
`refereeRewardCents` | number
`qualifySpendCents` | number
`holdDays` | number
`referred` | [RefereeStatus](RefereeStatus.md)

## Example

```typescript
import type { Referral } from '@deeprelay/sdk'

// TODO: Update the object below with actual values
const example = {
  "code": GPU-7KQ2-M4XP,
  "inviteUrl": https://deeprelay.ai/r/GPU-7KQ2-M4XP,
  "pending": null,
  "qualified": null,
  "settled": null,
  "earnedCents": null,
  "rewardCents": null,
  "refereeRewardCents": null,
  "qualifySpendCents": null,
  "holdDays": null,
  "referred": null,
} satisfies Referral

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as Referral
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


