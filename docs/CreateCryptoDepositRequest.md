
# CreateCryptoDepositRequest


## Properties

Name | Type
------------ | -------------
`amountCents` | number
`chain` | string
`asset` | string

## Example

```typescript
import type { CreateCryptoDepositRequest } from '@deeprelay/sdk'

// TODO: Update the object below with actual values
const example = {
  "amountCents": null,
  "chain": null,
  "asset": null,
} satisfies CreateCryptoDepositRequest

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as CreateCryptoDepositRequest
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


