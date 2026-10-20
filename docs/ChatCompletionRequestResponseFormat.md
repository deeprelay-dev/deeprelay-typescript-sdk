
# ChatCompletionRequestResponseFormat

Constrain the reply format. Gated per model: `json_object` needs \"response_format\" in the model\'s supported_parameters, and a strict `json_schema` needs \"structured_outputs\". A model without the capability returns 400 unsupported_parameter naming the models that have it. A non-strict json_schema on a model with only \"response_format\" is served as json_object and reported as `response_format:downgraded` in x-deeprelay-ignored-params. The relay never emulates JSON mode by prompting. 

## Properties

Name | Type
------------ | -------------
`type` | string
`jsonSchema` | [JSONSchemaFormat](JSONSchemaFormat.md)

## Example

```typescript
import type { ChatCompletionRequestResponseFormat } from '@deeprelay/sdk'

// TODO: Update the object below with actual values
const example = {
  "type": null,
  "jsonSchema": null,
} satisfies ChatCompletionRequestResponseFormat

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as ChatCompletionRequestResponseFormat
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


