
# ApiKeyCreate


## Properties

Name | Type
------------ | -------------
`name` | string
`scopes` | { [key: string]: any; }
`budgetCents` | number
`allowedModels` | Array&lt;string&gt;
`fallbackModels` | Array&lt;string&gt;
`rateLimitRps` | number
`rateLimitBurst` | number
`expiresAt` | Date

## Example

```typescript
import type { ApiKeyCreate } from '@deeprelay/sdk'

// TODO: Update the object below with actual values
const example = {
  "name": null,
  "scopes": null,
  "budgetCents": null,
  "allowedModels": null,
  "fallbackModels": null,
  "rateLimitRps": null,
  "rateLimitBurst": null,
  "expiresAt": null,
} satisfies ApiKeyCreate

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as ApiKeyCreate
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


