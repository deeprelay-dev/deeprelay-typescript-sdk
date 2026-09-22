# BillingApi

All URIs are relative to *https://api.deeprelay.ai/v1*

| Method | HTTP request | Description |
|------------- | ------------- | -------------|
| [**createCryptoDeposit**](BillingApi.md#createcryptodepositoperation) | **POST** /billing/deposits/crypto | Create a stablecoin deposit |
| [**getBalance**](BillingApi.md#getbalance) | **GET** /billing/balance | Get the org credit balance |
| [**getDeposit**](BillingApi.md#getdeposit) | **GET** /billing/deposits/{id} | Get one stablecoin deposit |
| [**getSpendingLimit**](BillingApi.md#getspendinglimit) | **GET** /billing/spending-limit | Get the org spending limit |
| [**getSubscription**](BillingApi.md#getsubscription) | **GET** /billing/subscription | Get the org subscription status and quota usage |
| [**listDeposits**](BillingApi.md#listdeposits) | **GET** /billing/deposits | List stablecoin deposits |
| [**updateSpendingLimit**](BillingApi.md#updatespendinglimitoperation) | **PUT** /billing/spending-limit | Set the org spending limit |



## createCryptoDeposit

> CryptoDeposit createCryptoDeposit(createCryptoDepositRequest)

Create a stablecoin deposit

Creates a deposit intent and returns the payment address and the exact token amount to send. Requires the &#x60;billing:write&#x60; scope; any member of the organization may add funds. Send the exact &#x60;pay_amount&#x60; of &#x60;asset&#x60; on &#x60;chain&#x60; and no other network — funds sent on a different network are not detected automatically. Returns 404 when stablecoin deposits are not enabled for this deployment. 

### Example

```ts
import {
  Configuration,
  BillingApi,
} from '@deeprelay/sdk';
import type { CreateCryptoDepositOperationRequest } from '@deeprelay/sdk';

async function example() {
  console.log("🚀 Testing @deeprelay/sdk SDK...");
  const config = new Configuration({ 
    // Configure HTTP bearer authorization: bearerAuth
    accessToken: "YOUR BEARER TOKEN",
  });
  const api = new BillingApi(config);

  const body = {
    // CreateCryptoDepositRequest
    createCryptoDepositRequest: ...,
  } satisfies CreateCryptoDepositOperationRequest;

  try {
    const data = await api.createCryptoDeposit(body);
    console.log(data);
  } catch (error) {
    console.error(error);
  }
}

// Run the test
example().catch(console.error);
```

### Parameters


| Name | Type | Description  | Notes |
|------------- | ------------- | ------------- | -------------|
| **createCryptoDepositRequest** | [CreateCryptoDepositRequest](CreateCryptoDepositRequest.md) |  | |

### Return type

[**CryptoDeposit**](CryptoDeposit.md)

### Authorization

[bearerAuth](../README.md#bearerAuth)

### HTTP request headers

- **Content-Type**: `application/json`
- **Accept**: `application/json`, `application/problem+json`


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **201** | Created |  -  |
| **400** | &#x60;validation-error&#x60; — &#x60;amount_cents&#x60; is below the configured minimum. &#x60;unsupported-chain-asset&#x60; — the chain/asset pair is not available. &#x60;invalid-request&#x60; — malformed JSON body.  |  -  |
| **403** | &#x60;org-frozen&#x60; — the organization cannot add funds; contact support. |  -  |
| **404** | Error response (RFC 7807) |  -  |
| **429** | Rate limit exceeded (RFC 7807). Retry-After header indicates seconds to wait. |  * Retry-After - Seconds the client should wait before retrying. <br>  |
| **503** | &#x60;payment-source-unavailable&#x60; — deposits are temporarily unavailable; retry shortly. |  -  |
| **0** | Error response (RFC 7807) |  -  |

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


## getBalance

> Balance getBalance()

Get the org credit balance

Returns the organization\&#39;s credit balance, its auto-pay configuration, and the live burn rate. Requires the &#x60;billing:read&#x60; scope. The organization is taken from the authenticated API key, never from a parameter.  Divide &#x60;balance_cents&#x60; by &#x60;burn_cents_per_hour&#x60; for the remaining runway in hours. The quotient is undefined in three cases a caller must keep apart: &#x60;burn_cents_per_hour&#x60; is 0 (nothing running, so the balance funds unbounded idle time), it is &#x60;null&#x60; (the burn rate could not be determined — NOT the same as idle), or the balance is already at or below zero.  This is the balance itself — for spend against a configured cap see &#x60;/billing/spending-limit&#x60;, and for past consumption see &#x60;/usage&#x60;. 

### Example

```ts
import {
  Configuration,
  BillingApi,
} from '@deeprelay/sdk';
import type { GetBalanceRequest } from '@deeprelay/sdk';

async function example() {
  console.log("🚀 Testing @deeprelay/sdk SDK...");
  const config = new Configuration({ 
    // Configure HTTP bearer authorization: bearerAuth
    accessToken: "YOUR BEARER TOKEN",
  });
  const api = new BillingApi(config);

  try {
    const data = await api.getBalance();
    console.log(data);
  } catch (error) {
    console.error(error);
  }
}

// Run the test
example().catch(console.error);
```

### Parameters

This endpoint does not need any parameter.

### Return type

[**Balance**](Balance.md)

### Authorization

[bearerAuth](../README.md#bearerAuth)

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: `application/json`, `application/problem+json`


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | OK |  -  |
| **429** | Rate limit exceeded (RFC 7807). Retry-After header indicates seconds to wait. |  * Retry-After - Seconds the client should wait before retrying. <br>  |
| **0** | Error response (RFC 7807) |  -  |

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


## getDeposit

> CryptoDeposit getDeposit(id)

Get one stablecoin deposit

Returns a single deposit belonging to the caller\&#39;s organization. Requires the &#x60;billing:read&#x60; scope. A deposit belonging to another organization returns the same &#x60;404 deposit-not-found&#x60; as one that does not exist — deliberately, so this endpoint cannot be used to test whether a deposit id is real. Also 404 when stablecoin deposits are not enabled for this deployment. 

### Example

```ts
import {
  Configuration,
  BillingApi,
} from '@deeprelay/sdk';
import type { GetDepositRequest } from '@deeprelay/sdk';

async function example() {
  console.log("🚀 Testing @deeprelay/sdk SDK...");
  const config = new Configuration({ 
    // Configure HTTP bearer authorization: bearerAuth
    accessToken: "YOUR BEARER TOKEN",
  });
  const api = new BillingApi(config);

  const body = {
    // string | The deposit id.
    id: id_example,
  } satisfies GetDepositRequest;

  try {
    const data = await api.getDeposit(body);
    console.log(data);
  } catch (error) {
    console.error(error);
  }
}

// Run the test
example().catch(console.error);
```

### Parameters


| Name | Type | Description  | Notes |
|------------- | ------------- | ------------- | -------------|
| **id** | `string` | The deposit id. | [Defaults to `undefined`] |

### Return type

[**CryptoDeposit**](CryptoDeposit.md)

### Authorization

[bearerAuth](../README.md#bearerAuth)

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: `application/json`, `application/problem+json`


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | OK |  -  |
| **404** | &#x60;deposit-not-found&#x60; — no such deposit, or it belongs to another organization. &#x60;not-found&#x60; — the feature is not enabled.  |  -  |
| **429** | Rate limit exceeded (RFC 7807). Retry-After header indicates seconds to wait. |  * Retry-After - Seconds the client should wait before retrying. <br>  |
| **0** | Error response (RFC 7807) |  -  |

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


## getSpendingLimit

> SpendingLimit getSpendingLimit()

Get the org spending limit

Returns the organization\&#39;s monthly spending limit and opt-in daily spend cap, with the current month and day spend. Requires the &#x60;billing:read&#x60; scope. Returns 404 when no limit is configured. 

### Example

```ts
import {
  Configuration,
  BillingApi,
} from '@deeprelay/sdk';
import type { GetSpendingLimitRequest } from '@deeprelay/sdk';

async function example() {
  console.log("🚀 Testing @deeprelay/sdk SDK...");
  const config = new Configuration({ 
    // Configure HTTP bearer authorization: bearerAuth
    accessToken: "YOUR BEARER TOKEN",
  });
  const api = new BillingApi(config);

  try {
    const data = await api.getSpendingLimit();
    console.log(data);
  } catch (error) {
    console.error(error);
  }
}

// Run the test
example().catch(console.error);
```

### Parameters

This endpoint does not need any parameter.

### Return type

[**SpendingLimit**](SpendingLimit.md)

### Authorization

[bearerAuth](../README.md#bearerAuth)

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: `application/json`, `application/problem+json`


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | OK |  -  |
| **404** | Error response (RFC 7807) |  -  |
| **429** | Rate limit exceeded (RFC 7807). Retry-After header indicates seconds to wait. |  * Retry-After - Seconds the client should wait before retrying. <br>  |
| **0** | Error response (RFC 7807) |  -  |

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


## getSubscription

> Subscription getSubscription()

Get the org subscription status and quota usage

Returns the organization\&#39;s flat-tier subscription: whether it is entitled, the current billing period, the plan\&#39;s configured quota, and — for an entitled subscription — consumption against the four limits the server enforces on every request. Requires the &#x60;billing:read&#x60; scope. The organization is taken from the authenticated API key, never from a parameter.  An organization that never subscribed is NOT an error. It gets 200 with &#x60;subscribed: false&#x60;, &#x60;status: \&quot;none\&quot;&#x60; and the quota the plan would provide, so a client can answer \&quot;what does the plan include\&quot; without a second endpoint and without an error path.  Read &#x60;subscribed&#x60;, not &#x60;status&#x60;, to decide whether the plan applies: &#x60;status&#x60; carries the billing provider\&#39;s vocabulary, and the two can disagree — an &#x60;active&#x60; subscription just past its period end still entitles for a short grace window (renewal-webhook lag), while &#x60;past_due&#x60; and &#x60;canceled&#x60; never entitle.  &#x60;usage&#x60; is present only for an entitled subscription whose meter could be read. An absent &#x60;usage&#x60; NEVER means \&quot;nothing used\&quot; — reading it as zero would report a full quota to an organization that has none left.  This is the plan\&#39;s meter. For pay-as-you-go credit see &#x60;/billing/balance&#x60;, for spend against a self-set cap see &#x60;/billing/spending-limit&#x60;, and for past consumption see &#x60;/usage&#x60;. 

### Example

```ts
import {
  Configuration,
  BillingApi,
} from '@deeprelay/sdk';
import type { GetSubscriptionRequest } from '@deeprelay/sdk';

async function example() {
  console.log("🚀 Testing @deeprelay/sdk SDK...");
  const config = new Configuration({ 
    // Configure HTTP bearer authorization: bearerAuth
    accessToken: "YOUR BEARER TOKEN",
  });
  const api = new BillingApi(config);

  try {
    const data = await api.getSubscription();
    console.log(data);
  } catch (error) {
    console.error(error);
  }
}

// Run the test
example().catch(console.error);
```

### Parameters

This endpoint does not need any parameter.

### Return type

[**Subscription**](Subscription.md)

### Authorization

[bearerAuth](../README.md#bearerAuth)

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: `application/json`, `application/problem+json`


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | OK |  -  |
| **429** | Rate limit exceeded (RFC 7807). Retry-After header indicates seconds to wait. |  * Retry-After - Seconds the client should wait before retrying. <br>  |
| **0** | Error response (RFC 7807) |  -  |

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


## listDeposits

> ListDeposits200Response listDeposits()

List stablecoin deposits

Returns the organization\&#39;s stablecoin deposits, newest first, capped at 50. Requires the &#x60;billing:read&#x60; scope. The organization is taken from the authenticated API key, never from a parameter. Returns 404 when stablecoin deposits are not enabled for this deployment. 

### Example

```ts
import {
  Configuration,
  BillingApi,
} from '@deeprelay/sdk';
import type { ListDepositsRequest } from '@deeprelay/sdk';

async function example() {
  console.log("🚀 Testing @deeprelay/sdk SDK...");
  const config = new Configuration({ 
    // Configure HTTP bearer authorization: bearerAuth
    accessToken: "YOUR BEARER TOKEN",
  });
  const api = new BillingApi(config);

  try {
    const data = await api.listDeposits();
    console.log(data);
  } catch (error) {
    console.error(error);
  }
}

// Run the test
example().catch(console.error);
```

### Parameters

This endpoint does not need any parameter.

### Return type

[**ListDeposits200Response**](ListDeposits200Response.md)

### Authorization

[bearerAuth](../README.md#bearerAuth)

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: `application/json`, `application/problem+json`


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | OK |  -  |
| **404** | Error response (RFC 7807) |  -  |
| **429** | Rate limit exceeded (RFC 7807). Retry-After header indicates seconds to wait. |  * Retry-After - Seconds the client should wait before retrying. <br>  |
| **0** | Error response (RFC 7807) |  -  |

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


## updateSpendingLimit

> SpendingLimit updateSpendingLimit(updateSpendingLimitRequest)

Set the org spending limit

Sets the monthly spending limit and optionally sets or clears the opt-in daily spend cap. Requires the &#x60;billing:write&#x60; scope AND org-admin privileges (a non-admin member gets 403). &#x60;daily_limit_dollars&#x60; uses pointer semantics: omit to leave the cap unchanged, 0 to clear it, a positive value to set it. 

### Example

```ts
import {
  Configuration,
  BillingApi,
} from '@deeprelay/sdk';
import type { UpdateSpendingLimitOperationRequest } from '@deeprelay/sdk';

async function example() {
  console.log("🚀 Testing @deeprelay/sdk SDK...");
  const config = new Configuration({ 
    // Configure HTTP bearer authorization: bearerAuth
    accessToken: "YOUR BEARER TOKEN",
  });
  const api = new BillingApi(config);

  const body = {
    // UpdateSpendingLimitRequest
    updateSpendingLimitRequest: ...,
  } satisfies UpdateSpendingLimitOperationRequest;

  try {
    const data = await api.updateSpendingLimit(body);
    console.log(data);
  } catch (error) {
    console.error(error);
  }
}

// Run the test
example().catch(console.error);
```

### Parameters


| Name | Type | Description  | Notes |
|------------- | ------------- | ------------- | -------------|
| **updateSpendingLimitRequest** | [UpdateSpendingLimitRequest](UpdateSpendingLimitRequest.md) |  | |

### Return type

[**SpendingLimit**](SpendingLimit.md)

### Authorization

[bearerAuth](../README.md#bearerAuth)

### HTTP request headers

- **Content-Type**: `application/json`
- **Accept**: `application/json`, `application/problem+json`


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | OK |  -  |
| **403** | Error response (RFC 7807) |  -  |
| **422** | Error response (RFC 7807) |  -  |
| **429** | Rate limit exceeded (RFC 7807). Retry-After header indicates seconds to wait. |  * Retry-After - Seconds the client should wait before retrying. <br>  |
| **0** | Error response (RFC 7807) |  -  |

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)

