
# AlertSettings


## Properties

Name | Type
------------ | -------------
`balanceThresholdCents` | number
`email` | [AlertEmailToggles](AlertEmailToggles.md)
`updatedAt` | Date
`note` | string

## Example

```typescript
import type { AlertSettings } from '@deeprelay/sdk'

// TODO: Update the object below with actual values
const example = {
  "balanceThresholdCents": null,
  "email": null,
  "updatedAt": null,
  "note": null,
} satisfies AlertSettings

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as AlertSettings
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


