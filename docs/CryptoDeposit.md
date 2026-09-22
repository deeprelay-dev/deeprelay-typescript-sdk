
# CryptoDeposit

A stablecoin deposit. Mirrors the Go DTO field for field. Like that struct, this schema deliberately has NO payment-processor property — the processor is an implementation detail and is structurally absent from the customer contract, not merely filtered out. 

## Properties

Name | Type
------------ | -------------
`depositId` | string
`status` | string
`chain` | string
`asset` | string
`payAddress` | string
`payAmount` | string
`amountUsdCents` | number
`creditedCents` | number
`txHash` | string
`expiresAt` | Date
`createdAt` | Date

## Example

```typescript
import type { CryptoDeposit } from '@deeprelay/sdk'

// TODO: Update the object below with actual values
const example = {
  "depositId": null,
  "status": null,
  "chain": null,
  "asset": null,
  "payAddress": null,
  "payAmount": null,
  "amountUsdCents": null,
  "creditedCents": null,
  "txHash": null,
  "expiresAt": null,
  "createdAt": null,
} satisfies CryptoDeposit

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as CryptoDeposit
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


