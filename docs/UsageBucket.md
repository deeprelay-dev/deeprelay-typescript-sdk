
# UsageBucket

One `/usage` row. Every row carries `bucket_start`, `gpu_seconds` and `cost_cents`. When the request set `modality` or `model` the row is an inference-usage row: it also carries `modality`, `model`, `prompt_tokens`, `completion_tokens` and `image_count` (aggregating every serverless inference call in the bucket for that modality and model), and `gpu_seconds` is always 0. Otherwise it is an instance-usage row, carrying `instance_id` / `gpu_type` when `group_by` asked for them. 

## Properties

Name | Type
------------ | -------------
`bucketStart` | Date
`instanceId` | string
`gpuType` | string
`gpuSeconds` | number
`costCents` | number
`modality` | string
`model` | string
`promptTokens` | number
`completionTokens` | number
`imageCount` | number

## Example

```typescript
import type { UsageBucket } from '@deeprelay/sdk'

// TODO: Update the object below with actual values
const example = {
  "bucketStart": null,
  "instanceId": null,
  "gpuType": null,
  "gpuSeconds": null,
  "costCents": null,
  "modality": null,
  "model": null,
  "promptTokens": null,
  "completionTokens": null,
  "imageCount": null,
} satisfies UsageBucket

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as UsageBucket
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


