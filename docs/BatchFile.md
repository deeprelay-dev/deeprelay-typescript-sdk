
# BatchFile

A batch file object: an input you uploaded (`batch`) or a result file written for a finished batch (`batch_output`, `batch_error`). The storage location is an internal detail and is intentionally absent from this schema (privacy-by-omission, D6).

## Properties

Name | Type
------------ | -------------
`id` | string
`object` | string
`bytes` | number
`createdAt` | number
`expiresAt` | number
`filename` | string
`purpose` | string

## Example

```typescript
import type { BatchFile } from '@deeprelay/sdk'

// TODO: Update the object below with actual values
const example = {
  "id": null,
  "object": null,
  "bytes": null,
  "createdAt": null,
  "expiresAt": null,
  "filename": null,
  "purpose": null,
} satisfies BatchFile

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as BatchFile
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


