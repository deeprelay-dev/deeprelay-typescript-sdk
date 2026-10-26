# BillingApi

All URIs are relative to *https://api.deeprelay.ai/v1*

| Method | HTTP request | Description |
|------------- | ------------- | -------------|
| [**createCryptoDeposit**](BillingApi.md#createcryptodepositoperation) | **POST** /billing/deposits/crypto | Create a stablecoin deposit |
| [**createSubscriptionCheckout**](BillingApi.md#createsubscriptioncheckout) | **POST** /billing/subscription/checkout | Start a subscription checkout session |
| [**createSubscriptionPortal**](BillingApi.md#createsubscriptionportal) | **POST** /billing/subscription/portal | Open the billing portal to cancel or manage the subscription |
| [**deleteSpendingLimit**](BillingApi.md#deletespendinglimit) | **DELETE** /billing/spending-limit | Clear the org spending limit |
| [**getBalance**](BillingApi.md#getbalance) | **GET** /billing/balance | Get the org credit balance |
| [**getDeposit**](BillingApi.md#getdeposit) | **GET** /billing/deposits/{id} | Get one stablecoin deposit |
| [**getReferral**](BillingApi.md#getreferral) | **GET** /referrals | Get the org referral code, invite link, terms and stats |
| [**getSpendingLimit**](BillingApi.md#getspendinglimit) | **GET** /billing/spending-limit | Get the org spending limit |
| [**getSubscription**](BillingApi.md#getsubscription) | **GET** /billing/subscription | Get the org subscription status and quota usage |
| [**listDeposits**](BillingApi.md#listdeposits) | **GET** /billing/deposits | List stablecoin deposits |
| [**updateSpendingLimit**](BillingApi.md#updatespendinglimitoperation) | **PUT** /billing/spending-limit | Set the org spending limit |
| [**upgradeSubscription**](BillingApi.md#upgradesubscription) | **POST** /billing/subscription/upgrade | Upgrade the subscription to a bigger plan |



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
| **400** | &#x60;validation-error&#x60; — &#x60;amount_cents&#x60; is below the configured minimum. &#x60;unsupported-chain-asset&#x60; — the chain/asset pair is not available. &#x60;amount-below-minimum&#x60;: the amount is below the network\&#39;s current minimum, which moves with network fees; &#x60;detail&#x60; quotes it when known. Raise the amount or choose another chain. &#x60;invalid-request&#x60; — malformed JSON body.  |  -  |
| **403** | &#x60;org-frozen&#x60; — the organization cannot add funds; contact support. |  -  |
| **404** | Error response (RFC 7807) |  -  |
| **429** | Rate limit exceeded (RFC 7807). Retry-After header indicates seconds to wait. |  * Retry-After - Seconds the client should wait before retrying. <br>  |
| **503** | &#x60;payment-source-unavailable&#x60; — deposits are temporarily unavailable; retry shortly. |  -  |
| **0** | Error response (RFC 7807) |  -  |

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


## createSubscriptionCheckout

> SubscriptionCheckoutSession createSubscriptionCheckout(subscriptionCheckoutRequest)

Start a subscription checkout session

Opens a hosted checkout session for a subscription plan and returns its URL. Requires the &#x60;billing:write&#x60; scope AND organization-admin privileges — subscribing spends organization money.  This endpoint does NOT subscribe anyone. Checkout is a hosted page that needs a browser and a card, so the caller\&#39;s job is to put the returned URL in front of a human. The subscription becomes active when payment completes, which is not synchronous with this call: poll &#x60;/billing/subscription&#x60; to confirm.  &#x60;success_url&#x60; and &#x60;cancel_url&#x60; are optional and fall back to the deployment\&#39;s configured redirects, which is what lets a command-line client start a purchase without having any URLs of its own. An empty request body is valid and means \&quot;use every default\&quot;. When sent, they must be on the deployment\&#39;s dashboard origin, else 422 &#x60;validation_failed&#x60;.  &#x60;plan_key&#x60; names the plan to buy: &#x60;flat&#x60; (Base, the default when the field is omitted) or &#x60;plus&#x60;. It pins the plan the client DISPLAYED — an unknown key, or a plan this deployment does not offer, is a 400 rather than a silent purchase of a different tier. The &#x60;plans&#x60; array on &#x60;/billing/subscription&#x60; lists the accepted keys.  One subscription per organization: a second checkout while an entitling subscription exists is a 409. To move an existing subscription to a bigger plan use &#x60;/billing/subscription/upgrade&#x60;.  &#x60;method&#x60; picks how the plan is paid: &#x60;card&#x60; (dollars, card or Link; the default) or &#x60;upi&#x60; (rupees, UPI AutoPay, India). On an organization that already subscribes, an explicit &#x60;method&#x60; in the other currency is a switch, not a second subscription: the link saves the new card or UPI AutoPay mandate (nothing is charged), and once that completes the same plan is moved to the new currency, first charged on the current renewal date (that month is already paid). The answer then carries &#x60;switch_to&#x60; and &#x60;first_charge_at&#x60;. A switch is refused (409) within two days of renewal, while the plan is set to cancel, while an upgrade waits on its UPI payment, and in the currency the plan already uses. While new payments are paused on the organization after several declined cards, a new checkout (a switch included) is refused with 429 &#x60;checkout_paused&#x60; and a Retry-After; renewing a plan billed through the previous payment account is never refused. 

### Example

```ts
import {
  Configuration,
  BillingApi,
} from '@deeprelay/sdk';
import type { CreateSubscriptionCheckoutRequest } from '@deeprelay/sdk';

async function example() {
  console.log("🚀 Testing @deeprelay/sdk SDK...");
  const config = new Configuration({ 
    // Configure HTTP bearer authorization: bearerAuth
    accessToken: "YOUR BEARER TOKEN",
  });
  const api = new BillingApi(config);

  const body = {
    // SubscriptionCheckoutRequest (optional)
    subscriptionCheckoutRequest: ...,
  } satisfies CreateSubscriptionCheckoutRequest;

  try {
    const data = await api.createSubscriptionCheckout(body);
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
| **subscriptionCheckoutRequest** | [SubscriptionCheckoutRequest](SubscriptionCheckoutRequest.md) |  | [Optional] |

### Return type

[**SubscriptionCheckoutSession**](SubscriptionCheckoutSession.md)

### Authorization

[bearerAuth](../README.md#bearerAuth)

### HTTP request headers

- **Content-Type**: `application/json`
- **Accept**: `application/json`, `application/problem+json`


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | OK |  -  |
| **403** | Not an organization admin |  -  |
| **409** | The organization already has an active subscription |  -  |
| **503** | Subscription billing is not configured on this deployment |  -  |
| **429** | Rate limit exceeded (RFC 7807). Retry-After header indicates seconds to wait. |  * Retry-After - Seconds the client should wait before retrying. <br>  |
| **0** | Error response (RFC 7807) |  -  |

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


## createSubscriptionPortal

> SubscriptionPortalSession createSubscriptionPortal(subscriptionPortalRequest)

Open the billing portal to cancel or manage the subscription

Returns a URL for the hosted billing portal: where a customer cancels the subscription, resumes one they cancelled, changes payment method, or downloads invoices. Requires the &#x60;billing:write&#x60; scope AND organization-admin privileges.  Cancellation lives here rather than on its own endpoint because it is one surface with the rest of the billing lifecycle. The common reason a subscription is about to lapse is a declined card, and the fix for that is a new card, not a cancellation — sending a customer somewhere that can only cancel would lose renewals.  Cancelling in the portal ends the subscription at the close of the current period; coverage continues until then and &#x60;/billing/subscription&#x60; reports &#x60;cancel_at_period_end: true&#x60;.  An organization that has never paid for anything gets 404: there is no billing account to manage, and this endpoint deliberately does not create one as a side effect of looking. 

### Example

```ts
import {
  Configuration,
  BillingApi,
} from '@deeprelay/sdk';
import type { CreateSubscriptionPortalRequest } from '@deeprelay/sdk';

async function example() {
  console.log("🚀 Testing @deeprelay/sdk SDK...");
  const config = new Configuration({ 
    // Configure HTTP bearer authorization: bearerAuth
    accessToken: "YOUR BEARER TOKEN",
  });
  const api = new BillingApi(config);

  const body = {
    // SubscriptionPortalRequest (optional)
    subscriptionPortalRequest: ...,
  } satisfies CreateSubscriptionPortalRequest;

  try {
    const data = await api.createSubscriptionPortal(body);
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
| **subscriptionPortalRequest** | [SubscriptionPortalRequest](SubscriptionPortalRequest.md) |  | [Optional] |

### Return type

[**SubscriptionPortalSession**](SubscriptionPortalSession.md)

### Authorization

[bearerAuth](../README.md#bearerAuth)

### HTTP request headers

- **Content-Type**: `application/json`
- **Accept**: `application/json`, `application/problem+json`


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | OK |  -  |
| **403** | Not an organization admin |  -  |
| **404** | The organization has no billing account yet |  -  |
| **503** | Subscription billing is not configured on this deployment |  -  |
| **429** | Rate limit exceeded (RFC 7807). Retry-After header indicates seconds to wait. |  * Retry-After - Seconds the client should wait before retrying. <br>  |
| **0** | Error response (RFC 7807) |  -  |

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


## deleteSpendingLimit

> deleteSpendingLimit()

Clear the org spending limit

Removes the organization\&#39;s monthly spending limit and daily spend cap entirely. Requires the &#x60;billing:write&#x60; scope AND org-admin privileges (a non-admin member gets 403). Returns 404 when no limit is configured. This is the only way to remove a limit through the API, because &#x60;PUT&#x60; floors &#x60;monthly_limit_dollars&#x60; at 1.00 and so cannot express \&quot;no limit\&quot;. 

### Example

```ts
import {
  Configuration,
  BillingApi,
} from '@deeprelay/sdk';
import type { DeleteSpendingLimitRequest } from '@deeprelay/sdk';

async function example() {
  console.log("🚀 Testing @deeprelay/sdk SDK...");
  const config = new Configuration({ 
    // Configure HTTP bearer authorization: bearerAuth
    accessToken: "YOUR BEARER TOKEN",
  });
  const api = new BillingApi(config);

  try {
    const data = await api.deleteSpendingLimit();
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

`void` (Empty response body)

### Authorization

[bearerAuth](../README.md#bearerAuth)

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: `application/problem+json`


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **204** | No Content |  -  |
| **403** | Error response (RFC 7807) |  -  |
| **404** | Error response (RFC 7807) |  -  |
| **429** | Rate limit exceeded (RFC 7807). Retry-After header indicates seconds to wait. |  * Retry-After - Seconds the client should wait before retrying. <br>  |
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


## getReferral

> Referral getReferral()

Get the org referral code, invite link, terms and stats

Returns the organization\&#39;s shareable referral code and invite link (minting the code on first read), the program terms, the referrer\&#39;s stats, and — when this organization itself signed up through someone else\&#39;s link — its own progress toward the referee reward. Requires the &#x60;billing:read&#x60; scope. The organization is taken from the authenticated API key, never from a parameter.  The program: share the invite link; once a friend who signed up through it has made &#x60;qualify_deposit_cents&#x60; of net real deposits (card, auto-pay or crypto, less refunds), the referrer receives &#x60;reward_cents&#x60; and the friend receives &#x60;referee_reward_cents&#x60;, both as non-withdrawable credit, after a &#x60;hold_days&#x60; chargeback hold. Both rewards are reversed if the qualifying deposit is later refunded. The deposit commission is retired and &#x60;commission_pct&#x60; is 0; when it is non-zero the referrer also earns that percent of every real deposit the friend makes. &#x60;commission_earned_cents&#x60; still reports commission earned before retirement. Program rewards never apply to the subscription. The terms ride on the wire so a client never hard-codes the amounts.  &#x60;referred&#x60; is ABSENT (not null) for an organization nobody referred — key on its presence. This is the same contract the dashboard\&#39;s referral card reads. 

### Example

```ts
import {
  Configuration,
  BillingApi,
} from '@deeprelay/sdk';
import type { GetReferralRequest } from '@deeprelay/sdk';

async function example() {
  console.log("🚀 Testing @deeprelay/sdk SDK...");
  const config = new Configuration({ 
    // Configure HTTP bearer authorization: bearerAuth
    accessToken: "YOUR BEARER TOKEN",
  });
  const api = new BillingApi(config);

  try {
    const data = await api.getReferral();
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

[**Referral**](Referral.md)

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

Returns the organization\&#39;s subscription: whether it is entitled, the current billing period, the plan it is on and that plan\&#39;s configured quota, and — for an entitled subscription — consumption against the limits the server enforces on every request. Requires the &#x60;billing:read&#x60; scope. The organization is taken from the authenticated API key, never from a parameter.  &#x60;plan&#x60; and &#x60;quota&#x60; describe the plan the organization IS on (the Base plan for an organization that never subscribed). &#x60;plans&#x60; lists every plan this deployment offers — Base, then Plus — each with its price and quota, so a client can render an upgrade offer without a second call.  An organization that never subscribed is NOT an error. It gets 200 with &#x60;subscribed: false&#x60;, &#x60;status: \&quot;none\&quot;&#x60; and the quota the Base plan would provide, so a client can answer \&quot;what does the plan include\&quot; without a second endpoint and without an error path.  Read &#x60;subscribed&#x60;, not &#x60;status&#x60;, to decide whether the plan applies: &#x60;status&#x60; carries the billing provider\&#39;s vocabulary, and the two can disagree — an &#x60;active&#x60; subscription just past its period end still entitles for a short grace window (renewal-webhook lag), while &#x60;past_due&#x60; and &#x60;canceled&#x60; never entitle.  &#x60;usage&#x60; is present only for an entitled subscription whose meter could be read. An absent &#x60;usage&#x60; NEVER means \&quot;nothing used\&quot; — reading it as zero would report a full quota to an organization that has none left.  This is the plan\&#39;s meter. For pay-as-you-go credit see &#x60;/billing/balance&#x60;, for spend against a self-set cap see &#x60;/billing/spending-limit&#x60;, and for past consumption see &#x60;/usage&#x60;. 

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


## upgradeSubscription

> Subscription upgradeSubscription(subscriptionUpgradeRequest)

Upgrade the subscription to a bigger plan

Moves the organization\&#39;s EXISTING subscription onto a bigger plan. Requires the &#x60;billing:write&#x60; scope AND organization-admin privileges — an upgrade charges the organization\&#39;s card on file.  Unlike checkout, no hosted page is involved: the subscription\&#39;s price is swapped, the new plan\&#39;s FULL price is charged immediately (whenever in the cycle the upgrade happens), and a new billing period starts now. There is no credit for the unused remainder of the old plan\&#39;s period, and the usage meters start from zero on the new plan because every quota window is summed over the current period. The response is the post-upgrade subscription, in the same shape as &#x60;/billing/subscription&#x60;.  &#x60;plan_key&#x60; is required and names the target plan (&#x60;plus&#x60;). The target must be bigger than the plan the organization is on: upgrading to the current plan or to a smaller one is a 409 &#x60;not_an_upgrade&#x60; — downgrades go through the billing portal. An organization with no entitling subscription gets 409 &#x60;not_subscribed&#x60; and should use checkout instead. A subscription already set to end at the period close is refused with 409 &#x60;subscription_cancelling&#x60; (the upgrade would start a new period and move that end date); resume it in the portal first.  If the charge cannot be collected (card declined, no payment method) the call is a 402 &#x60;payment_failed&#x60; and NOTHING changes — the organization stays on its current plan. Fix the card in the billing portal and retry. 

### Example

```ts
import {
  Configuration,
  BillingApi,
} from '@deeprelay/sdk';
import type { UpgradeSubscriptionRequest } from '@deeprelay/sdk';

async function example() {
  console.log("🚀 Testing @deeprelay/sdk SDK...");
  const config = new Configuration({ 
    // Configure HTTP bearer authorization: bearerAuth
    accessToken: "YOUR BEARER TOKEN",
  });
  const api = new BillingApi(config);

  const body = {
    // SubscriptionUpgradeRequest
    subscriptionUpgradeRequest: ...,
  } satisfies UpgradeSubscriptionRequest;

  try {
    const data = await api.upgradeSubscription(body);
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
| **subscriptionUpgradeRequest** | [SubscriptionUpgradeRequest](SubscriptionUpgradeRequest.md) |  | |

### Return type

[**Subscription**](Subscription.md)

### Authorization

[bearerAuth](../README.md#bearerAuth)

### HTTP request headers

- **Content-Type**: `application/json`
- **Accept**: `application/json`, `application/problem+json`


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | OK — the subscription after the upgrade |  -  |
| **400** | Unknown plan_key, or a plan this deployment does not offer |  -  |
| **402** | Payment for the new plan failed; the current plan is unchanged |  -  |
| **403** | Not an organization admin |  -  |
| **409** | &#x60;not_subscribed&#x60; — no active subscription to upgrade (use checkout); &#x60;not_an_upgrade&#x60; — the target is the current plan or a smaller one; &#x60;subscription_cancelling&#x60; — the subscription is set to end at the period close (resume it in the portal first) |  -  |
| **422** | plan_key is missing |  -  |
| **503** | Subscription billing is not configured on this deployment |  -  |
| **429** | Rate limit exceeded (RFC 7807). Retry-After header indicates seconds to wait. |  * Retry-After - Seconds the client should wait before retrying. <br>  |
| **0** | Error response (RFC 7807) |  -  |

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)

