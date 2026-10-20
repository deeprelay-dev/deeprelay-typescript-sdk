
# ApiKeyCreated

The new key\'s metadata plus its secret (`key`), returned exactly once. The same fields as `ApiKey`, plus `key`.

## Properties

Name | Type
------------ | -------------
`apiKeyId` | string
`name` | string
`keyPrefix` | string
`last4` | string
`scopes` | [ApiKeyScopes](ApiKeyScopes.md)
`budgetCents` | number
`budgetUsedMicroCents` | number
`budgetResetsAt` | Date
`allowedModels` | Array&lt;string&gt;
`staleModels` | Array&lt;string&gt;
`rateLimitRps` | number
`rateLimitBurst` | number
`expiresAt` | Date
`createdAt` | Date
`lastUsedAt` | Date
`revokedAt` | Date
`key` | string

## Example

```typescript
import type { ApiKeyCreated } from '@deeprelay/sdk'

// TODO: Update the object below with actual values
const example = {
  "apiKeyId": null,
  "name": null,
  "keyPrefix": null,
  "last4": null,
  "scopes": null,
  "budgetCents": null,
  "budgetUsedMicroCents": null,
  "budgetResetsAt": null,
  "allowedModels": null,
  "staleModels": null,
  "rateLimitRps": null,
  "rateLimitBurst": null,
  "expiresAt": null,
  "createdAt": null,
  "lastUsedAt": null,
  "revokedAt": null,
  "key": null,
} satisfies ApiKeyCreated

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as ApiKeyCreated
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


