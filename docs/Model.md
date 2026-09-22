
# Model


## Properties

Name | Type
------------ | -------------
`id` | string
`object` | string
`created` | number
`ownedBy` | string
`author` | string
`modality` | string
`category` | string
`contextLength` | number
`supportedParameters` | Array&lt;string&gt;
`parameters` | [Array&lt;ModelParametersInner&gt;](ModelParametersInner.md)
`pricing` | [ModelPricing](ModelPricing.md)
`aliases` | Array&lt;string&gt;
`fineTunable` | boolean
`fineTuneBaseModel` | string
`planCovered` | boolean
`status` | string

## Example

```typescript
import type { Model } from '@deeprelay/sdk'

// TODO: Update the object below with actual values
const example = {
  "id": null,
  "object": null,
  "created": null,
  "ownedBy": null,
  "author": null,
  "modality": null,
  "category": null,
  "contextLength": null,
  "supportedParameters": null,
  "parameters": null,
  "pricing": null,
  "aliases": null,
  "fineTunable": null,
  "fineTuneBaseModel": null,
  "planCovered": null,
  "status": null,
} satisfies Model

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as Model
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


