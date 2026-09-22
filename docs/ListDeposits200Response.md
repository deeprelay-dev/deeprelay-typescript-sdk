
# ListDeposits200Response


## Properties

Name | Type
------------ | -------------
`deposits` | [Array&lt;CryptoDeposit&gt;](CryptoDeposit.md)
`minDepositCents` | number

## Example

```typescript
import type { ListDeposits200Response } from '@deeprelay/sdk'

// TODO: Update the object below with actual values
const example = {
  "deposits": null,
  "minDepositCents": 500,
} satisfies ListDeposits200Response

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as ListDeposits200Response
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


