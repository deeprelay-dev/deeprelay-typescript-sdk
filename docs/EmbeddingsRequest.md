
# EmbeddingsRequest


## Properties

Name | Type
------------ | -------------
`model` | string
`input` | [EmbeddingsRequestInput](EmbeddingsRequestInput.md)
`encodingFormat` | string
`dimensions` | number
`user` | string

## Example

```typescript
import type { EmbeddingsRequest } from '@deeprelay/sdk'

// TODO: Update the object below with actual values
const example = {
  "model": null,
  "input": null,
  "encodingFormat": null,
  "dimensions": null,
  "user": null,
} satisfies EmbeddingsRequest

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as EmbeddingsRequest
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


