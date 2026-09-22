
# ImagesGenerationsRequest


## Properties

Name | Type
------------ | -------------
`model` | string
`prompt` | string
`n` | number
`size` | string
`responseFormat` | string

## Example

```typescript
import type { ImagesGenerationsRequest } from '@deeprelay/sdk'

// TODO: Update the object below with actual values
const example = {
  "model": null,
  "prompt": null,
  "n": null,
  "size": null,
  "responseFormat": null,
} satisfies ImagesGenerationsRequest

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as ImagesGenerationsRequest
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


