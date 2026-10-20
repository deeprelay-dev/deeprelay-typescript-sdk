
# UsagePromptTokensDetails

Present whenever the upstream reported prompt-cache usage, including a reported 0. Absent means the upstream did not report it. 

## Properties

Name | Type
------------ | -------------
`cachedTokens` | number

## Example

```typescript
import type { UsagePromptTokensDetails } from '@deeprelay/sdk'

// TODO: Update the object below with actual values
const example = {
  "cachedTokens": null,
} satisfies UsagePromptTokensDetails

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as UsagePromptTokensDetails
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


