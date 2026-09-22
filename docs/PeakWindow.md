
# PeakWindow

One daily UTC time range during which a model\'s peak rates apply.

## Properties

Name | Type
------------ | -------------
`start` | string
`end` | string

## Example

```typescript
import type { PeakWindow } from '@deeprelay/sdk'

// TODO: Update the object below with actual values
const example = {
  "start": null,
  "end": null,
} satisfies PeakWindow

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as PeakWindow
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


