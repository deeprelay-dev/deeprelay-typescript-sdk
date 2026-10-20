
# ChatCompletionRequestToolChoice

How the model should pick a tool: the strings \"none\", \"auto\" or \"required\", or an object naming one function. Requires a non-empty tools array unless it is \"none\". 

## Properties

Name | Type
------------ | -------------
`type` | string
`_function` | [ToolChoiceFunctionFunction](ToolChoiceFunctionFunction.md)

## Example

```typescript
import type { ChatCompletionRequestToolChoice } from '@deeprelay/sdk'

// TODO: Update the object below with actual values
const example = {
  "type": null,
  "_function": null,
} satisfies ChatCompletionRequestToolChoice

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as ChatCompletionRequestToolChoice
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


