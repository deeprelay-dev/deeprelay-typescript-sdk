
# BatchLimits

Every per-organization batch limit with its current value.

## Properties

Name | Type
------------ | -------------
`maxLines` | number
`maxFileBytes` | number
`maxLineBytes` | number
`maxActiveBatches` | number
`activeBatches` | number
`maxFiles` | number
`files` | number
`queuedTokenCap` | number
`queuedTokens` | number
`maxAgeHours` | number
`retentionDays` | number

## Example

```typescript
import type { BatchLimits } from '@deeprelay/sdk'

// TODO: Update the object below with actual values
const example = {
  "maxLines": null,
  "maxFileBytes": null,
  "maxLineBytes": null,
  "maxActiveBatches": null,
  "activeBatches": null,
  "maxFiles": null,
  "files": null,
  "queuedTokenCap": null,
  "queuedTokens": null,
  "maxAgeHours": null,
  "retentionDays": null,
} satisfies BatchLimits

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as BatchLimits
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


