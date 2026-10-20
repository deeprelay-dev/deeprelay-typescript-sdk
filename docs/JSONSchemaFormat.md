
# JSONSchemaFormat

The schema is forwarded byte-for-byte. It may be at most 64 KiB and nested at most 32 levels deep; larger or deeper schemas return 400 unsupported_parameter (param response_format). 

## Properties

Name | Type
------------ | -------------
`name` | string
`description` | string
`schema` | { [key: string]: any; }
`strict` | boolean

## Example

```typescript
import type { JSONSchemaFormat } from '@deeprelay/sdk'

// TODO: Update the object below with actual values
const example = {
  "name": null,
  "description": null,
  "schema": null,
  "strict": null,
} satisfies JSONSchemaFormat

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as JSONSchemaFormat
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


