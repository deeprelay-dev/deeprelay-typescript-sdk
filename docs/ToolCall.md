
# ToolCall

A function call the model emitted.

## Properties

Name | Type
------------ | -------------
`index` | number
`id` | string
`type` | string
`_function` | [ToolCallFunction](ToolCallFunction.md)

## Example

```typescript
import type { ToolCall } from '@deeprelay/sdk'

// TODO: Update the object below with actual values
const example = {
  "index": null,
  "id": null,
  "type": null,
  "_function": null,
} satisfies ToolCall

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as ToolCall
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


