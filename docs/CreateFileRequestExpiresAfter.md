
# CreateFileRequestExpiresAfter

Optional file lifetime, sent as the form fields `expires_after[anchor]` and `expires_after[seconds]`. Absent means 30 days after upload.

## Properties

Name | Type
------------ | -------------
`anchor` | string
`seconds` | number

## Example

```typescript
import type { CreateFileRequestExpiresAfter } from '@deeprelay/sdk'

// TODO: Update the object below with actual values
const example = {
  "anchor": null,
  "seconds": null,
} satisfies CreateFileRequestExpiresAfter

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as CreateFileRequestExpiresAfter
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


