
# VideoJob


## Properties

Name | Type
------------ | -------------
`id` | string
`object` | string
`model` | string
`status` | string
`progress` | number
`size` | string
`seconds` | number
`createdAt` | number
`completedAt` | number
`expiresAt` | number
`error` | string
`costCents` | number

## Example

```typescript
import type { VideoJob } from '@deeprelay/sdk'

// TODO: Update the object below with actual values
const example = {
  "id": null,
  "object": null,
  "model": null,
  "status": null,
  "progress": null,
  "size": null,
  "seconds": null,
  "createdAt": null,
  "completedAt": null,
  "expiresAt": null,
  "error": null,
  "costCents": null,
} satisfies VideoJob

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as VideoJob
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


