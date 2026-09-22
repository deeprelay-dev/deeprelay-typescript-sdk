
# InferencePreflight

The verdict for one (organization, model) pair: what would happen if the model were invoked right now. 

## Properties

Name | Type
------------ | -------------
`model` | string
`verdict` | string
`reason` | string
`message` | string
`planCovered` | boolean
`subscribed` | boolean
`funded` | boolean

## Example

```typescript
import type { InferencePreflight } from '@deeprelay/sdk'

// TODO: Update the object below with actual values
const example = {
  "model": null,
  "verdict": null,
  "reason": null,
  "message": null,
  "planCovered": null,
  "subscribed": null,
  "funded": null,
} satisfies InferencePreflight

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as InferencePreflight
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


