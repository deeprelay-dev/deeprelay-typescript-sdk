
# ModelPricing


## Properties

Name | Type
------------ | -------------
`currency` | string
`inputPer1mTokensCents` | number
`outputPer1mTokensCents` | number
`cachedInputPer1mTokensMicrocents` | number
`cachedInputPer1mTokensCents` | number
`perImageCents` | number
`perImageMicrocents` | number
`perMpxlMicrocents` | number
`perVideoMicrocents` | number
`perVideoSecondCents` | number
`perVideoSecondMicrocents` | number
`period` | string
`peakWindowsUtc` | [Array&lt;PeakWindow&gt;](PeakWindow.md)
`peak` | [ModelRate](ModelRate.md)
`offPeak` | [ModelRate](ModelRate.md)

## Example

```typescript
import type { ModelPricing } from '@deeprelay/sdk'

// TODO: Update the object below with actual values
const example = {
  "currency": null,
  "inputPer1mTokensCents": null,
  "outputPer1mTokensCents": null,
  "cachedInputPer1mTokensMicrocents": null,
  "cachedInputPer1mTokensCents": null,
  "perImageCents": null,
  "perImageMicrocents": null,
  "perMpxlMicrocents": null,
  "perVideoMicrocents": null,
  "perVideoSecondCents": null,
  "perVideoSecondMicrocents": null,
  "period": null,
  "peakWindowsUtc": null,
  "peak": null,
  "offPeak": null,
} satisfies ModelPricing

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as ModelPricing
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


