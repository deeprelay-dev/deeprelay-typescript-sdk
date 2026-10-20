# ApiKeysApi

All URIs are relative to *https://api.deeprelay.ai/v1*

| Method | HTTP request | Description |
|------------- | ------------- | -------------|
| [**createApiKey**](ApiKeysApi.md#createapikey) | **POST** /api-keys | Create an API key |
| [**getApiKey**](ApiKeysApi.md#getapikey) | **GET** /api-keys/{id} | Get an API key |
| [**listApiKeys**](ApiKeysApi.md#listapikeys) | **GET** /api-keys | List API keys |
| [**revokeApiKey**](ApiKeysApi.md#revokeapikey) | **DELETE** /api-keys/{id} | Revoke an API key |
| [**updateApiKey**](ApiKeysApi.md#updateapikey) | **PATCH** /api-keys/{id} | Update an API key\&#39;s name or limits |



## createApiKey

> ApiKeyCreated createApiKey(apiKeyCreate)

Create an API key

Mints a key. The response is the only place the secret (&#x60;key&#x60;) appears; store it then, because it cannot be read again.  Requires the &#x60;keys:manage&#x60; capability: a &#x60;full_access&#x60; key, or a key whose scopes grant &#x60;{\&quot;keys\&quot;: \&quot;write\&quot;}&#x60;. Any other key gets 403 &#x60;keys_manage_required&#x60;. A key can never mint a key stronger than itself: scopes it does not hold answer 403 &#x60;scope_exceeds_caller&#x60;, and a minting key that has a budget, a model allowlist, a rate limit or an expiry passes each down as an upper bound (422 &#x60;validation_failed&#x60; naming the &#x60;field&#x60;). Only an org admin can mint a &#x60;full_access&#x60; key. 

### Example

```ts
import {
  Configuration,
  ApiKeysApi,
} from '@deeprelay/sdk';
import type { CreateApiKeyRequest } from '@deeprelay/sdk';

async function example() {
  console.log("🚀 Testing @deeprelay/sdk SDK...");
  const config = new Configuration({ 
    // Configure HTTP bearer authorization: bearerAuth
    accessToken: "YOUR BEARER TOKEN",
  });
  const api = new ApiKeysApi(config);

  const body = {
    // ApiKeyCreate
    apiKeyCreate: ...,
  } satisfies CreateApiKeyRequest;

  try {
    const data = await api.createApiKey(body);
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
| **apiKeyCreate** | [ApiKeyCreate](ApiKeyCreate.md) |  | |

### Return type

[**ApiKeyCreated**](ApiKeyCreated.md)

### Authorization

[bearerAuth](../README.md#bearerAuth)

### HTTP request headers

- **Content-Type**: `application/json`
- **Accept**: `application/json`, `application/problem+json`


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **201** | Created. The response is sent with &#x60;Cache-Control: no-store&#x60;. |  -  |
| **400** | Error response (RFC 7807) |  -  |
| **403** | &#x60;keys_manage_required&#x60; (the calling key cannot manage keys), &#x60;scope_exceeds_caller&#x60; (the requested scopes exceed the calling key\&#39;s own) or &#x60;forbidden&#x60; (only an org admin can mint a &#x60;full_access&#x60; key). |  -  |
| **422** | Error response (RFC 7807) |  -  |
| **429** | Rate limit exceeded (RFC 7807). Retry-After header indicates seconds to wait. |  * Retry-After - Seconds the client should wait before retrying. <br>  |
| **0** | Error response (RFC 7807) |  -  |

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


## getApiKey

> ApiKey getApiKey(id)

Get an API key

Returns one key. A key the caller cannot see answers 404. Requires the &#x60;keys:read&#x60; scope. 

### Example

```ts
import {
  Configuration,
  ApiKeysApi,
} from '@deeprelay/sdk';
import type { GetApiKeyRequest } from '@deeprelay/sdk';

async function example() {
  console.log("🚀 Testing @deeprelay/sdk SDK...");
  const config = new Configuration({ 
    // Configure HTTP bearer authorization: bearerAuth
    accessToken: "YOUR BEARER TOKEN",
  });
  const api = new ApiKeysApi(config);

  const body = {
    // string
    id: 38400000-8cf0-11bd-b23e-10b96e4ef00d,
  } satisfies GetApiKeyRequest;

  try {
    const data = await api.getApiKey(body);
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
| **id** | `string` |  | [Defaults to `undefined`] |

### Return type

[**ApiKey**](ApiKey.md)

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


## listApiKeys

> ApiKeyList listApiKeys()

List API keys

Lists the organization\&#39;s API keys with their limits and current budget use. An org admin\&#39;s key and a &#x60;full_access&#x60; key see every key in the organization; any other key sees only the keys its owner created. The secret is never returned here. Requires the &#x60;keys:read&#x60; scope. 

### Example

```ts
import {
  Configuration,
  ApiKeysApi,
} from '@deeprelay/sdk';
import type { ListApiKeysRequest } from '@deeprelay/sdk';

async function example() {
  console.log("🚀 Testing @deeprelay/sdk SDK...");
  const config = new Configuration({ 
    // Configure HTTP bearer authorization: bearerAuth
    accessToken: "YOUR BEARER TOKEN",
  });
  const api = new ApiKeysApi(config);

  try {
    const data = await api.listApiKeys();
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

[**ApiKeyList**](ApiKeyList.md)

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


## revokeApiKey

> revokeApiKey(id, idempotencyKey)

Revoke an API key

Revokes the key immediately; it cannot be restored. Requires the &#x60;keys:manage&#x60; capability (403 &#x60;keys_manage_required&#x60; otherwise); a member can only revoke keys they created. 

### Example

```ts
import {
  Configuration,
  ApiKeysApi,
} from '@deeprelay/sdk';
import type { RevokeApiKeyRequest } from '@deeprelay/sdk';

async function example() {
  console.log("🚀 Testing @deeprelay/sdk SDK...");
  const config = new Configuration({ 
    // Configure HTTP bearer authorization: bearerAuth
    accessToken: "YOUR BEARER TOKEN",
  });
  const api = new ApiKeysApi(config);

  const body = {
    // string
    id: 38400000-8cf0-11bd-b23e-10b96e4ef00d,
    // string (optional)
    idempotencyKey: idempotencyKey_example,
  } satisfies RevokeApiKeyRequest;

  try {
    const data = await api.revokeApiKey(body);
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
| **id** | `string` |  | [Defaults to `undefined`] |
| **idempotencyKey** | `string` |  | [Optional] [Defaults to `undefined`] |

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
| **204** | Revoked |  -  |
| **403** | Error response (RFC 7807) |  -  |
| **404** | Error response (RFC 7807) |  -  |
| **429** | Rate limit exceeded (RFC 7807). Retry-After header indicates seconds to wait. |  * Retry-After - Seconds the client should wait before retrying. <br>  |
| **0** | Error response (RFC 7807) |  -  |

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


## updateApiKey

> ApiKey updateApiKey(id, apiKeyUpdate, idempotencyKey)

Update an API key\&#39;s name or limits

Changes a key\&#39;s name, budget, model allowlist, rate limit or expiry. An absent field is left unchanged; an explicit &#x60;null&#x60; clears &#x60;budget_cents&#x60;, &#x60;allowed_models&#x60; or &#x60;expires_at&#x60;. &#x60;scopes&#x60; cannot be changed after minting, and unknown fields are refused (422), so a typo never looks like a successful change. Requires the &#x60;keys:manage&#x60; capability (403 &#x60;keys_manage_required&#x60; otherwise); a member can only change keys they created. 

### Example

```ts
import {
  Configuration,
  ApiKeysApi,
} from '@deeprelay/sdk';
import type { UpdateApiKeyRequest } from '@deeprelay/sdk';

async function example() {
  console.log("🚀 Testing @deeprelay/sdk SDK...");
  const config = new Configuration({ 
    // Configure HTTP bearer authorization: bearerAuth
    accessToken: "YOUR BEARER TOKEN",
  });
  const api = new ApiKeysApi(config);

  const body = {
    // string
    id: 38400000-8cf0-11bd-b23e-10b96e4ef00d,
    // ApiKeyUpdate
    apiKeyUpdate: ...,
    // string (optional)
    idempotencyKey: idempotencyKey_example,
  } satisfies UpdateApiKeyRequest;

  try {
    const data = await api.updateApiKey(body);
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
| **id** | `string` |  | [Defaults to `undefined`] |
| **apiKeyUpdate** | [ApiKeyUpdate](ApiKeyUpdate.md) |  | |
| **idempotencyKey** | `string` |  | [Optional] [Defaults to `undefined`] |

### Return type

[**ApiKey**](ApiKey.md)

### Authorization

[bearerAuth](../README.md#bearerAuth)

### HTTP request headers

- **Content-Type**: `application/json`
- **Accept**: `application/json`, `application/problem+json`


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | OK |  -  |
| **400** | Error response (RFC 7807) |  -  |
| **403** | Error response (RFC 7807) |  -  |
| **404** | Error response (RFC 7807) |  -  |
| **422** | Error response (RFC 7807) |  -  |
| **429** | Rate limit exceeded (RFC 7807). Retry-After header indicates seconds to wait. |  * Retry-After - Seconds the client should wait before retrying. <br>  |
| **0** | Error response (RFC 7807) |  -  |

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)

