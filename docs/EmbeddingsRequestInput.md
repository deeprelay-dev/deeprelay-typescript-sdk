
# EmbeddingsRequestInput

Text to embed: either a single string or an array of up to 2048 strings. Token-id arrays are not supported. The per-request ceiling is bounded so the response stays under 64 MiB — about 680 inputs at 4096 dimensions, fewer at a larger `dimensions` value; an over-limit batch is rejected with 400 invalid_request_error whose message states the limit, before any processing.

## Properties

Name | Type
------------ | -------------

## Example

```typescript
import type { EmbeddingsRequestInput } from '@deeprelay/sdk'

// TODO: Update the object below with actual values
const example = {
} satisfies EmbeddingsRequestInput

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as EmbeddingsRequestInput
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


