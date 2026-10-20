
# CostDetails

How this call was priced, in USD (exact decimals, up to 8 places). list_price_equivalent = plan_covered_amount + charged_amount. A call is either fully covered by the subscription or fully charged: there is no partial coverage. 

## Properties

Name | Type
------------ | -------------
`listPriceEquivalent` | number
`planCoveredAmount` | number
`chargedAmount` | number
`quotaUnitsUsed` | number
`cacheSavings` | number

## Example

```typescript
import type { CostDetails } from '@deeprelay/sdk'

// TODO: Update the object below with actual values
const example = {
  "listPriceEquivalent": null,
  "planCoveredAmount": null,
  "chargedAmount": null,
  "quotaUnitsUsed": null,
  "cacheSavings": null,
} satisfies CostDetails

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as CostDetails
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


