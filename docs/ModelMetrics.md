
# ModelMetrics

Measured performance over a rolling window, from deeprelay\'s own customer traffic only. A figure is omitted (never zero) when it has too few samples behind it; the counts and minimums are always present so a reader can tell why.

## Properties

Name | Type
------------ | -------------
`windowDays` | number
`asOf` | Date
`sampleCount` | number
`streamSampleCount` | number
`minSamples` | number
`minStreamSamples` | number
`ttftP50Ms` | number
`tokensPerSecondP50` | number
`successRate` | number
`insufficientData` | boolean
`precision` | string

## Example

```typescript
import type { ModelMetrics } from '@deeprelay/sdk'

// TODO: Update the object below with actual values
const example = {
  "windowDays": null,
  "asOf": null,
  "sampleCount": null,
  "streamSampleCount": null,
  "minSamples": null,
  "minStreamSamples": null,
  "ttftP50Ms": null,
  "tokensPerSecondP50": null,
  "successRate": null,
  "insufficientData": null,
  "precision": null,
} satisfies ModelMetrics

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as ModelMetrics
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


