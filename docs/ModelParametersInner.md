
# ModelParametersInner


## Properties

Name | Type
------------ | -------------
`name` | string
`type` | string
`_enum` | Array&lt;string&gt;
`min` | number
`max` | number
`_default` | any

## Example

```typescript
import type { ModelParametersInner } from '@deeprelay/sdk'

// TODO: Update the object below with actual values
const example = {
  "name": null,
  "type": null,
  "_enum": null,
  "min": null,
  "max": null,
  "_default": null,
} satisfies ModelParametersInner

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as ModelParametersInner
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


