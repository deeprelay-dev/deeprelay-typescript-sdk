
# ModelRate

One per-1M-token rate triple, in rounded cents and exact micro-cents (1e-6 cent). Prefer the micro-cent fields for arithmetic; cached rates are routinely sub-cent and their cents field is then omitted.

## Properties

Name | Type
------------ | -------------
`inputPer1mTokensCents` | number
`inputPer1mTokensMicrocents` | number
`cachedInputPer1mTokensCents` | number
`cachedInputPer1mTokensMicrocents` | number
`outputPer1mTokensCents` | number
`outputPer1mTokensMicrocents` | number

## Example

```typescript
import type { ModelRate } from '@deeprelay/sdk'

// TODO: Update the object below with actual values
const example = {
  "inputPer1mTokensCents": null,
  "inputPer1mTokensMicrocents": null,
  "cachedInputPer1mTokensCents": null,
  "cachedInputPer1mTokensMicrocents": null,
  "outputPer1mTokensCents": null,
  "outputPer1mTokensMicrocents": null,
} satisfies ModelRate

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as ModelRate
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


