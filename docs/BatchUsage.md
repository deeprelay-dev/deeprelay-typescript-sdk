
# BatchUsage

Token usage summed over the batch\'s billed lines.

## Properties

Name | Type
------------ | -------------
`inputTokens` | number
`inputTokensDetails` | [BatchUsageInputTokensDetails](BatchUsageInputTokensDetails.md)
`outputTokens` | number
`outputTokensDetails` | [BatchUsageOutputTokensDetails](BatchUsageOutputTokensDetails.md)
`totalTokens` | number

## Example

```typescript
import type { BatchUsage } from '@deeprelay/sdk'

// TODO: Update the object below with actual values
const example = {
  "inputTokens": null,
  "inputTokensDetails": null,
  "outputTokens": null,
  "outputTokensDetails": null,
  "totalTokens": null,
} satisfies BatchUsage

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as BatchUsage
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


