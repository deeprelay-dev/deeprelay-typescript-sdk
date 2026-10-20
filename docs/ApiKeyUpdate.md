
# ApiKeyUpdate

Send only the fields to change. `null` clears `budget_cents`, `allowed_models` or `expires_at`. `scopes` cannot be changed.

## Properties

Name | Type
------------ | -------------
`name` | string
`budgetCents` | number
`allowedModels` | Array&lt;string&gt;
`rateLimitRps` | number
`rateLimitBurst` | number
`expiresAt` | Date

## Example

```typescript
import type { ApiKeyUpdate } from '@deeprelay/sdk'

// TODO: Update the object below with actual values
const example = {
  "name": null,
  "budgetCents": null,
  "allowedModels": null,
  "rateLimitRps": null,
  "rateLimitBurst": null,
  "expiresAt": null,
} satisfies ApiKeyUpdate

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as ApiKeyUpdate
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


