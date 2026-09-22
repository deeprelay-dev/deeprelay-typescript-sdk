
# UsageBucket


## Properties

Name | Type
------------ | -------------
`bucketStart` | Date
`instanceId` | string
`gpuType` | string
`gpuSeconds` | number
`costCents` | number

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


