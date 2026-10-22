
# RequestAttempt

One model in a request\'s backup-model trail.

## Properties

Name | Type
------------ | -------------
`model` | string
`outcome` | string
`reason` | string
`durationMs` | number
`ttftMs` | number
`tries` | number

## Example

```typescript
import type { RequestAttempt } from '@deeprelay/sdk'

// TODO: Update the object below with actual values
const example = {
  "model": null,
  "outcome": null,
  "reason": null,
  "durationMs": null,
  "ttftMs": null,
  "tries": null,
} satisfies RequestAttempt

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as RequestAttempt
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


