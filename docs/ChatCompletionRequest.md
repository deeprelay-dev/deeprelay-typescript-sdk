
# ChatCompletionRequest


## Properties

Name | Type
------------ | -------------
`model` | string
`messages` | [Array&lt;ChatMessage&gt;](ChatMessage.md)
`temperature` | number
`maxTokens` | number
`stream` | boolean
`streamOptions` | [StreamOptions](StreamOptions.md)

## Example

```typescript
import type { ChatCompletionRequest } from '@deeprelay/sdk'

// TODO: Update the object below with actual values
const example = {
  "model": null,
  "messages": null,
  "temperature": null,
  "maxTokens": null,
  "stream": null,
  "streamOptions": null,
} satisfies ChatCompletionRequest

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as ChatCompletionRequest
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


