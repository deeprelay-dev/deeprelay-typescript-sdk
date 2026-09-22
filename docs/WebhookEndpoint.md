
# WebhookEndpoint


## Properties

Name | Type
------------ | -------------
`id` | string
`url` | string
`secret` | string
`eventTypes` | Array&lt;string&gt;
`enabled` | boolean
`createdAt` | Date

## Example

```typescript
import type { WebhookEndpoint } from '@deeprelay/sdk'

// TODO: Update the object below with actual values
const example = {
  "id": null,
  "url": null,
  "secret": null,
  "eventTypes": null,
  "enabled": null,
  "createdAt": null,
} satisfies WebhookEndpoint

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as WebhookEndpoint
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


