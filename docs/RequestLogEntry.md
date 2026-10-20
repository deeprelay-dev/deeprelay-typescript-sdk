
# RequestLogEntry

One inference call as the request log records it. Never carries prompt or completion content. Optional numeric fields are omitted when they do not apply (for example token counts on a rejected call).

## Properties

Name | Type
------------ | -------------
`requestId` | string
`clientRequestId` | string
`occurredAt` | Date
`surface` | string
`model` | string
`keyId` | string
`keyName` | string
`keyPrefix` | string
`status` | string
`httpStatus` | number
`errorCode` | string
`finishReason` | string
`promptTokens` | number
`completionTokens` | number
`cachedTokens` | number
`reasoningTokens` | number
`quotaUnits` | number
`cost` | number
`costMicroCents` | number
`planCovered` | boolean
`ttftMs` | number
`durationMs` | number
`ignoredParams` | Array&lt;string&gt;
`hadToolCalls` | boolean
`imageCount` | number
`videoSeconds` | number
`suppressedCount` | number

## Example

```typescript
import type { RequestLogEntry } from '@deeprelay/sdk'

// TODO: Update the object below with actual values
const example = {
  "requestId": null,
  "clientRequestId": null,
  "occurredAt": null,
  "surface": null,
  "model": null,
  "keyId": null,
  "keyName": null,
  "keyPrefix": null,
  "status": null,
  "httpStatus": null,
  "errorCode": null,
  "finishReason": null,
  "promptTokens": null,
  "completionTokens": null,
  "cachedTokens": null,
  "reasoningTokens": null,
  "quotaUnits": null,
  "cost": null,
  "costMicroCents": null,
  "planCovered": null,
  "ttftMs": null,
  "durationMs": null,
  "ignoredParams": null,
  "hadToolCalls": null,
  "imageCount": null,
  "videoSeconds": null,
  "suppressedCount": null,
} satisfies RequestLogEntry

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as RequestLogEntry
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


