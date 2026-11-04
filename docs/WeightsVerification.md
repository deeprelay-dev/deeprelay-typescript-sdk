
# WeightsVerification

Present only for an open-weight chat model whose latest public fingerprint run passed: the run compared the relay\'s output distributions against independent deployments of the same weights and found them the same model. Derived from the newest run the public harness published (see `method_url`), through a short cache, and dropped once that run is older than 14 days. There is no negative value: a model the run did not verify, for any reason, simply has no `weights_verification` key.

## Properties

Name | Type
------------ | -------------
`status` | string
`weights` | string
`verifiedAt` | Date
`runId` | string
`runUrl` | string
`harnessVersion` | string
`references` | number
`methodUrl` | string

## Example

```typescript
import type { WeightsVerification } from '@deeprelay/sdk'

// TODO: Update the object below with actual values
const example = {
  "status": null,
  "weights": null,
  "verifiedAt": null,
  "runId": null,
  "runUrl": null,
  "harnessVersion": null,
  "references": null,
  "methodUrl": null,
} satisfies WeightsVerification

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as WeightsVerification
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


