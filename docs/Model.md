
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
`tier` | string
`contextLength` | number
`maxCompletionTokens` | number
`supportedParameters` | Array&lt;string&gt;
`webSearch` | boolean
`reasoningEfforts` | Array&lt;string&gt;
`parameters` | [Array&lt;ModelParametersInner&gt;](ModelParametersInner.md)
`pricing` | [ModelPricing](ModelPricing.md)
`aliases` | Array&lt;string&gt;
`fineTunable` | boolean
`fineTuneBaseModel` | string
`hfRepo` | string
`usageFactorMilli` | number
`planCovered` | boolean
`recommendedFor` | Array&lt;string&gt;
`codingAgentRank` | number
`status` | string
`metrics` | [ModelMetrics](ModelMetrics.md)

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
  "tier": null,
  "contextLength": null,
  "maxCompletionTokens": null,
  "supportedParameters": null,
  "webSearch": null,
  "reasoningEfforts": null,
  "parameters": null,
  "pricing": null,
  "aliases": null,
  "fineTunable": null,
  "fineTuneBaseModel": null,
  "hfRepo": null,
  "usageFactorMilli": null,
  "planCovered": null,
  "recommendedFor": null,
  "codingAgentRank": null,
  "status": null,
  "metrics": null,
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


