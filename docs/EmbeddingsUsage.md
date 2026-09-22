
# EmbeddingsUsage

Embeddings are billed on input tokens only, so this block carries no completion_tokens field — an embeddings call emits none, and total_tokens always equals prompt_tokens.

## Properties

Name | Type
------------ | -------------
`promptTokens` | number
`totalTokens` | number

## Example

```typescript
import type { EmbeddingsUsage } from '@deeprelay/sdk'

// TODO: Update the object below with actual values
const example = {
  "promptTokens": null,
  "totalTokens": null,
} satisfies EmbeddingsUsage

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as EmbeddingsUsage
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


