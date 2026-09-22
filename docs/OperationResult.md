
# OperationResult

Terminal-success payload. Carries the per-instance web-access coordinates — app_url for template deploys, terminal_url for instances provisioned with the browser web console, and the basic-auth username shared by both. The basic-auth PASSWORD is never included here — retrieve it via GET /instances/{id}?include=credentials (connection.app_password).

## Properties

Name | Type
------------ | -------------
`appUrl` | string
`terminalUrl` | string
`appBasicAuthUser` | string

## Example

```typescript
import type { OperationResult } from '@deeprelay/sdk'

// TODO: Update the object below with actual values
const example = {
  "appUrl": null,
  "terminalUrl": null,
  "appBasicAuthUser": null,
} satisfies OperationResult

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as OperationResult
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


