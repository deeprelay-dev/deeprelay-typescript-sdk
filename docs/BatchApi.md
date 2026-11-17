# BatchApi

All URIs are relative to *https://api.deeprelay.ai/v1*

| Method | HTTP request | Description |
|------------- | ------------- | -------------|
| [**cancelBatch**](BatchApi.md#cancelbatch) | **POST** /batches/{id}/cancel | Cancel a batch (OpenAI-compatible) |
| [**createBatch**](BatchApi.md#createbatchoperation) | **POST** /batches | Create an off-peak batch (OpenAI-compatible) |
| [**createFile**](BatchApi.md#createfile) | **POST** /files | Upload a batch input file (OpenAI-compatible) |
| [**deleteFile**](BatchApi.md#deletefile) | **DELETE** /files/{id} | Delete a batch file (OpenAI-compatible) |
| [**getBatchLimits**](BatchApi.md#getbatchlimits) | **GET** /batches/limits | Per-organization batch limits with current values |
| [**listBatches**](BatchApi.md#listbatches) | **GET** /batches | List batches, newest first (OpenAI-compatible) |
| [**listFiles**](BatchApi.md#listfiles) | **GET** /files | List batch files (OpenAI-compatible) |
| [**retrieveBatch**](BatchApi.md#retrievebatch) | **GET** /batches/{id} | Retrieve a batch (OpenAI-compatible) |
| [**retrieveFile**](BatchApi.md#retrievefile) | **GET** /files/{id} | Retrieve a batch file (OpenAI-compatible) |
| [**retrieveFileContent**](BatchApi.md#retrievefilecontent) | **GET** /files/{id}/content | Download a batch file\&#39;s content (JSONL) |



## cancelBatch

> Batch cancelBatch(id)

Cancel a batch (OpenAI-compatible)

Stops the batch\&#39;s queued lines at once. Lines already running finish and are billed; the output file holds every completed line and the error file lists the rest as &#x60;batch_cancelled&#x60;. The batch moves to &#x60;cancelling&#x60;, then &#x60;cancelled&#x60;.

### Example

```ts
import {
  Configuration,
  BatchApi,
} from '@deeprelay/sdk';
import type { CancelBatchRequest } from '@deeprelay/sdk';

async function example() {
  console.log("🚀 Testing @deeprelay/sdk SDK...");
  const config = new Configuration({ 
    // Configure HTTP bearer authorization: bearerAuth
    accessToken: "YOUR BEARER TOKEN",
  });
  const api = new BatchApi(config);

  const body = {
    // string
    id: id_example,
  } satisfies CancelBatchRequest;

  try {
    const data = await api.cancelBatch(body);
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

[**Batch**](Batch.md)

### Authorization

[bearerAuth](../README.md#bearerAuth)

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: `application/json`


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | The batch object (cancelling, or unchanged when finalizing or finished). |  -  |
| **401** | Missing or invalid API key (OpenAI error envelope). |  * X-Deeprelay-Error-Code -  <br>  |
| **404** | Model or resource not found (OpenAI error envelope). |  * X-Deeprelay-Error-Code -  <br>  |
| **429** | Rate limit or subscription quota exceeded (OpenAI error envelope). A per-key or per-IP rate limit (&#x60;rate_limit_exceeded&#x60;) carries Retry-After, the whole seconds to wait, rounded up (minimum 1), and retry-after-ms, the exact wait; both are the time until one request is allowed, not a full refill. A per-key denial also carries the x-ratelimit-*-requests headers. A subscription quota denial (&#x60;subscription_quota_exhausted&#x60;, raised only when the wallet cannot cover the pay-as-you-go fallback) carries &#x60;x-should-retry: false&#x60; and no Retry-After. When the tripped gate is a rolling 7-day cap (&#x60;param: weekly_input_tokens&#x60; or &#x60;param: weekly_output_tokens&#x60;), the error object also carries &#x60;quota_frees_at&#x60;, the RFC 3339 time the window frees enough capacity — the earlier of the two windows. &#x60;param&#x60; names the tripped gate: monthly_input_tokens, monthly_output_tokens, weekly_input_tokens, weekly_output_tokens, max_usage, input_overshoot (this request\&#39;s estimated input alone exceeds what is left in the tighter of the monthly and rolling 7-day input allowances), or output_overshoot (the same for the estimated output — the completion bound). On an overshoot the quota is not exhausted — send a smaller request (or a smaller max_tokens) or add credits. |  * X-Deeprelay-Requested-Model -  <br>  * X-Deeprelay-Fallback-Attempted -  <br>  * Retry-After - Seconds the client should wait before retrying. <br>  * retry-after-ms -  <br>  * x-ratelimit-limit-requests -  <br>  * x-ratelimit-remaining-requests -  <br>  * x-ratelimit-reset-requests -  <br>  * x-should-retry -  <br>  * X-Deeprelay-Error-Code -  <br>  |
| **500** | Internal server error (OpenAI error envelope). |  * X-Deeprelay-Error-Code -  <br>  |

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


## createBatch

> Batch createBatch(createBatchRequest)

Create an off-peak batch (OpenAI-compatible)

Submits an uploaded input file as a batch. deeprelay runs it in the model\&#39;s next off-peak window (at once when the model is off-peak now, or has no peak schedule) and bills each line at the rate in effect when it runs. Every line is checked first through the same validation a synchronous request gets; a batch with any invalid line is rejected whole with 400 &#x60;batch_validation_failed&#x60; naming the lines. One model and one endpoint per batch. The submit is gated on the batch\&#39;s estimated cost (input tokens plus &#x60;max_tokens&#x60; at the batch rate) with the same balance and spend checks as a synchronous request; the estimate is not a hold. Pay-as-you-go only: batch lines are never covered by a subscription plan.

### Example

```ts
import {
  Configuration,
  BatchApi,
} from '@deeprelay/sdk';
import type { CreateBatchOperationRequest } from '@deeprelay/sdk';

async function example() {
  console.log("🚀 Testing @deeprelay/sdk SDK...");
  const config = new Configuration({ 
    // Configure HTTP bearer authorization: bearerAuth
    accessToken: "YOUR BEARER TOKEN",
  });
  const api = new BatchApi(config);

  const body = {
    // CreateBatchRequest
    createBatchRequest: ...,
  } satisfies CreateBatchOperationRequest;

  try {
    const data = await api.createBatch(body);
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
| **createBatchRequest** | [CreateBatchRequest](CreateBatchRequest.md) |  | |

### Return type

[**Batch**](Batch.md)

### Authorization

[bearerAuth](../README.md#bearerAuth)

### HTTP request headers

- **Content-Type**: `application/json`
- **Accept**: `application/json`


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | The batch object. |  -  |
| **400** | &#x60;batch_validation_failed&#x60; (invalid lines, more than one model, a line &#x60;url&#x60; that differs from &#x60;endpoint&#x60;, &#x60;stream: true&#x60;, a server tool, a model with no off-peak time, or an input file that expires before the batch could finish), &#x60;batch_limit_exceeded&#x60; (active batches or the queued-token cap), &#x60;server_tool_unsupported&#x60;, &#x60;invalid_completion_window&#x60; (anything but &#x60;\&quot;24h\&quot;&#x60;) or &#x60;invalid_request&#x60;. OpenAI error envelope. |  -  |
| **401** | Missing or invalid API key (OpenAI error envelope). |  * X-Deeprelay-Error-Code -  <br>  |
| **402** | Insufficient balance or a spend limit reached (OpenAI error envelope, SERV-06): &#x60;insufficient_balance&#x60;, &#x60;daily_limit_reached&#x60;, &#x60;spending_limit_reached&#x60;, &#x60;api_key_budget_exceeded&#x60; (this API key\&#39;s monthly budget) or &#x60;member_spend_limit_reached&#x60; (the member\&#39;s monthly spend limit). Carries &#x60;x-should-retry: false&#x60;: the same request will not succeed until the wallet or the limit changes. |  * x-should-retry -  <br>  * X-Deeprelay-Error-Code -  <br>  |
| **403** | API key lacks the required scope (&#x60;insufficient_scope&#x60;), or the key has a model allowlist that does not include the requested model (&#x60;model_not_allowed_for_key&#x60;; also the answer for a model that does not exist, so a restricted key cannot probe the catalog). OpenAI error envelope. |  * X-Deeprelay-Error-Code -  <br>  |
| **404** | Model or resource not found (OpenAI error envelope). |  * X-Deeprelay-Error-Code -  <br>  |
| **413** | Request body too large (OpenAI error envelope, code request_too_large). |  * X-Deeprelay-Error-Code -  <br>  |
| **429** | Rate limit or subscription quota exceeded (OpenAI error envelope). A per-key or per-IP rate limit (&#x60;rate_limit_exceeded&#x60;) carries Retry-After, the whole seconds to wait, rounded up (minimum 1), and retry-after-ms, the exact wait; both are the time until one request is allowed, not a full refill. A per-key denial also carries the x-ratelimit-*-requests headers. A subscription quota denial (&#x60;subscription_quota_exhausted&#x60;, raised only when the wallet cannot cover the pay-as-you-go fallback) carries &#x60;x-should-retry: false&#x60; and no Retry-After. When the tripped gate is a rolling 7-day cap (&#x60;param: weekly_input_tokens&#x60; or &#x60;param: weekly_output_tokens&#x60;), the error object also carries &#x60;quota_frees_at&#x60;, the RFC 3339 time the window frees enough capacity — the earlier of the two windows. &#x60;param&#x60; names the tripped gate: monthly_input_tokens, monthly_output_tokens, weekly_input_tokens, weekly_output_tokens, max_usage, input_overshoot (this request\&#39;s estimated input alone exceeds what is left in the tighter of the monthly and rolling 7-day input allowances), or output_overshoot (the same for the estimated output — the completion bound). On an overshoot the quota is not exhausted — send a smaller request (or a smaller max_tokens) or add credits. |  * X-Deeprelay-Requested-Model -  <br>  * X-Deeprelay-Fallback-Attempted -  <br>  * Retry-After - Seconds the client should wait before retrying. <br>  * retry-after-ms -  <br>  * x-ratelimit-limit-requests -  <br>  * x-ratelimit-remaining-requests -  <br>  * x-ratelimit-reset-requests -  <br>  * x-should-retry -  <br>  * X-Deeprelay-Error-Code -  <br>  |
| **500** | Internal server error (OpenAI error envelope). |  * X-Deeprelay-Error-Code -  <br>  |

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


## createFile

> BatchFile createFile(purpose, file, expiresAfter)

Upload a batch input file (OpenAI-compatible)

Uploads a JSONL batch input file (&#x60;purpose&#x3D;batch&#x60;), one request per line in the OpenAI batch shape (&#x60;custom_id&#x60;, &#x60;method: POST&#x60;, &#x60;url&#x60;, &#x60;body&#x60;). The whole file is checked before anything is stored: a bad line is 400 &#x60;batch_validation_failed&#x60; naming the line numbers, a file over a size, line-count, line-size or stored-file limit is 400 &#x60;batch_limit_exceeded&#x60;, and any purpose other than &#x60;batch&#x60; is 400 &#x60;invalid_purpose&#x60;. A body over the file-size limit is 413 &#x60;request_too_large&#x60;. The stored file is encrypted at rest and deleted at &#x60;expires_at&#x60; (30 days by default) or on &#x60;DELETE /files/{id}&#x60;.

### Example

```ts
import {
  Configuration,
  BatchApi,
} from '@deeprelay/sdk';
import type { CreateFileRequest } from '@deeprelay/sdk';

async function example() {
  console.log("🚀 Testing @deeprelay/sdk SDK...");
  const config = new Configuration({ 
    // Configure HTTP bearer authorization: bearerAuth
    accessToken: "YOUR BEARER TOKEN",
  });
  const api = new BatchApi(config);

  const body = {
    // string
    purpose: purpose_example,
    // Blob | A JSONL file, one request per line.
    file: BINARY_DATA_HERE,
    // CreateFileRequestExpiresAfter (optional)
    expiresAfter: ...,
  } satisfies CreateFileRequest;

  try {
    const data = await api.createFile(body);
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
| **purpose** | `batch` |  | [Defaults to `undefined`] [Enum: batch] |
| **file** | `Blob` | A JSONL file, one request per line. | [Defaults to `undefined`] |
| **expiresAfter** | [CreateFileRequestExpiresAfter](CreateFileRequestExpiresAfter.md) |  | [Optional] [Defaults to `undefined`] |

### Return type

[**BatchFile**](BatchFile.md)

### Authorization

[bearerAuth](../README.md#bearerAuth)

### HTTP request headers

- **Content-Type**: `multipart/form-data`
- **Accept**: `application/json`


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | The uploaded file object. |  -  |
| **400** | &#x60;batch_validation_failed&#x60; (one or more lines are invalid; the message lists the line numbers), &#x60;batch_limit_exceeded&#x60; (a file, line or stored-file limit), &#x60;invalid_purpose&#x60;, &#x60;invalid_multipart&#x60;, &#x60;missing_file&#x60; or &#x60;invalid_request&#x60; (a bad &#x60;expires_after&#x60;). OpenAI error envelope. |  -  |
| **401** | Missing or invalid API key (OpenAI error envelope). |  * X-Deeprelay-Error-Code -  <br>  |
| **403** | API key lacks the required scope (&#x60;insufficient_scope&#x60;), or the key has a model allowlist that does not include the requested model (&#x60;model_not_allowed_for_key&#x60;; also the answer for a model that does not exist, so a restricted key cannot probe the catalog). OpenAI error envelope. |  * X-Deeprelay-Error-Code -  <br>  |
| **413** | Request body too large (OpenAI error envelope, code request_too_large). |  * X-Deeprelay-Error-Code -  <br>  |
| **429** | Rate limit or subscription quota exceeded (OpenAI error envelope). A per-key or per-IP rate limit (&#x60;rate_limit_exceeded&#x60;) carries Retry-After, the whole seconds to wait, rounded up (minimum 1), and retry-after-ms, the exact wait; both are the time until one request is allowed, not a full refill. A per-key denial also carries the x-ratelimit-*-requests headers. A subscription quota denial (&#x60;subscription_quota_exhausted&#x60;, raised only when the wallet cannot cover the pay-as-you-go fallback) carries &#x60;x-should-retry: false&#x60; and no Retry-After. When the tripped gate is a rolling 7-day cap (&#x60;param: weekly_input_tokens&#x60; or &#x60;param: weekly_output_tokens&#x60;), the error object also carries &#x60;quota_frees_at&#x60;, the RFC 3339 time the window frees enough capacity — the earlier of the two windows. &#x60;param&#x60; names the tripped gate: monthly_input_tokens, monthly_output_tokens, weekly_input_tokens, weekly_output_tokens, max_usage, input_overshoot (this request\&#39;s estimated input alone exceeds what is left in the tighter of the monthly and rolling 7-day input allowances), or output_overshoot (the same for the estimated output — the completion bound). On an overshoot the quota is not exhausted — send a smaller request (or a smaller max_tokens) or add credits. |  * X-Deeprelay-Requested-Model -  <br>  * X-Deeprelay-Fallback-Attempted -  <br>  * Retry-After - Seconds the client should wait before retrying. <br>  * retry-after-ms -  <br>  * x-ratelimit-limit-requests -  <br>  * x-ratelimit-remaining-requests -  <br>  * x-ratelimit-reset-requests -  <br>  * x-should-retry -  <br>  * X-Deeprelay-Error-Code -  <br>  |
| **500** | Internal server error (OpenAI error envelope). |  * X-Deeprelay-Error-Code -  <br>  |

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


## deleteFile

> BatchFileDeleted deleteFile(id)

Delete a batch file (OpenAI-compatible)

Deletes the file and its stored content immediately. There are no versioned or replicated copies of batch file content, so nothing is left to purge. The input file of a batch that is still queued or running cannot be deleted (409 &#x60;file_in_use&#x60;); cancel the batch first.

### Example

```ts
import {
  Configuration,
  BatchApi,
} from '@deeprelay/sdk';
import type { DeleteFileRequest } from '@deeprelay/sdk';

async function example() {
  console.log("🚀 Testing @deeprelay/sdk SDK...");
  const config = new Configuration({ 
    // Configure HTTP bearer authorization: bearerAuth
    accessToken: "YOUR BEARER TOKEN",
  });
  const api = new BatchApi(config);

  const body = {
    // string
    id: id_example,
  } satisfies DeleteFileRequest;

  try {
    const data = await api.deleteFile(body);
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

[**BatchFileDeleted**](BatchFileDeleted.md)

### Authorization

[bearerAuth](../README.md#bearerAuth)

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: `application/json`


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | The deletion result. |  -  |
| **401** | Missing or invalid API key (OpenAI error envelope). |  * X-Deeprelay-Error-Code -  <br>  |
| **404** | Model or resource not found (OpenAI error envelope). |  * X-Deeprelay-Error-Code -  <br>  |
| **409** | &#x60;file_in_use&#x60;: the file is the input of a batch that is still queued or running; cancel the batch first. OpenAI error envelope. |  * X-Deeprelay-Error-Code -  <br>  |
| **429** | Rate limit or subscription quota exceeded (OpenAI error envelope). A per-key or per-IP rate limit (&#x60;rate_limit_exceeded&#x60;) carries Retry-After, the whole seconds to wait, rounded up (minimum 1), and retry-after-ms, the exact wait; both are the time until one request is allowed, not a full refill. A per-key denial also carries the x-ratelimit-*-requests headers. A subscription quota denial (&#x60;subscription_quota_exhausted&#x60;, raised only when the wallet cannot cover the pay-as-you-go fallback) carries &#x60;x-should-retry: false&#x60; and no Retry-After. When the tripped gate is a rolling 7-day cap (&#x60;param: weekly_input_tokens&#x60; or &#x60;param: weekly_output_tokens&#x60;), the error object also carries &#x60;quota_frees_at&#x60;, the RFC 3339 time the window frees enough capacity — the earlier of the two windows. &#x60;param&#x60; names the tripped gate: monthly_input_tokens, monthly_output_tokens, weekly_input_tokens, weekly_output_tokens, max_usage, input_overshoot (this request\&#39;s estimated input alone exceeds what is left in the tighter of the monthly and rolling 7-day input allowances), or output_overshoot (the same for the estimated output — the completion bound). On an overshoot the quota is not exhausted — send a smaller request (or a smaller max_tokens) or add credits. |  * X-Deeprelay-Requested-Model -  <br>  * X-Deeprelay-Fallback-Attempted -  <br>  * Retry-After - Seconds the client should wait before retrying. <br>  * retry-after-ms -  <br>  * x-ratelimit-limit-requests -  <br>  * x-ratelimit-remaining-requests -  <br>  * x-ratelimit-reset-requests -  <br>  * x-should-retry -  <br>  * X-Deeprelay-Error-Code -  <br>  |
| **500** | Internal server error (OpenAI error envelope). |  * X-Deeprelay-Error-Code -  <br>  |

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


## getBatchLimits

> BatchLimits getBatchLimits()

Per-organization batch limits with current values

### Example

```ts
import {
  Configuration,
  BatchApi,
} from '@deeprelay/sdk';
import type { GetBatchLimitsRequest } from '@deeprelay/sdk';

async function example() {
  console.log("🚀 Testing @deeprelay/sdk SDK...");
  const config = new Configuration({ 
    // Configure HTTP bearer authorization: bearerAuth
    accessToken: "YOUR BEARER TOKEN",
  });
  const api = new BatchApi(config);

  try {
    const data = await api.getBatchLimits();
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

[**BatchLimits**](BatchLimits.md)

### Authorization

[bearerAuth](../README.md#bearerAuth)

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: `application/json`


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | Every batch limit and its current value. |  -  |
| **401** | Missing or invalid API key (OpenAI error envelope). |  * X-Deeprelay-Error-Code -  <br>  |
| **429** | Rate limit or subscription quota exceeded (OpenAI error envelope). A per-key or per-IP rate limit (&#x60;rate_limit_exceeded&#x60;) carries Retry-After, the whole seconds to wait, rounded up (minimum 1), and retry-after-ms, the exact wait; both are the time until one request is allowed, not a full refill. A per-key denial also carries the x-ratelimit-*-requests headers. A subscription quota denial (&#x60;subscription_quota_exhausted&#x60;, raised only when the wallet cannot cover the pay-as-you-go fallback) carries &#x60;x-should-retry: false&#x60; and no Retry-After. When the tripped gate is a rolling 7-day cap (&#x60;param: weekly_input_tokens&#x60; or &#x60;param: weekly_output_tokens&#x60;), the error object also carries &#x60;quota_frees_at&#x60;, the RFC 3339 time the window frees enough capacity — the earlier of the two windows. &#x60;param&#x60; names the tripped gate: monthly_input_tokens, monthly_output_tokens, weekly_input_tokens, weekly_output_tokens, max_usage, input_overshoot (this request\&#39;s estimated input alone exceeds what is left in the tighter of the monthly and rolling 7-day input allowances), or output_overshoot (the same for the estimated output — the completion bound). On an overshoot the quota is not exhausted — send a smaller request (or a smaller max_tokens) or add credits. |  * X-Deeprelay-Requested-Model -  <br>  * X-Deeprelay-Fallback-Attempted -  <br>  * Retry-After - Seconds the client should wait before retrying. <br>  * retry-after-ms -  <br>  * x-ratelimit-limit-requests -  <br>  * x-ratelimit-remaining-requests -  <br>  * x-ratelimit-reset-requests -  <br>  * x-should-retry -  <br>  * X-Deeprelay-Error-Code -  <br>  |
| **500** | Internal server error (OpenAI error envelope). |  * X-Deeprelay-Error-Code -  <br>  |

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


## listBatches

> BatchList listBatches(after, limit)

List batches, newest first (OpenAI-compatible)

### Example

```ts
import {
  Configuration,
  BatchApi,
} from '@deeprelay/sdk';
import type { ListBatchesRequest } from '@deeprelay/sdk';

async function example() {
  console.log("🚀 Testing @deeprelay/sdk SDK...");
  const config = new Configuration({ 
    // Configure HTTP bearer authorization: bearerAuth
    accessToken: "YOUR BEARER TOKEN",
  });
  const api = new BatchApi(config);

  const body = {
    // string (optional)
    after: after_example,
    // number (optional)
    limit: 56,
  } satisfies ListBatchesRequest;

  try {
    const data = await api.listBatches(body);
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
| **after** | `string` |  | [Optional] [Defaults to `undefined`] |
| **limit** | `number` |  | [Optional] [Defaults to `20`] |

### Return type

[**BatchList**](BatchList.md)

### Authorization

[bearerAuth](../README.md#bearerAuth)

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: `application/json`


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | A page of batch objects. |  -  |
| **400** | Invalid request (OpenAI error envelope). |  * X-Deeprelay-Requested-Model -  <br>  * X-Deeprelay-Fallback-Attempted -  <br>  * X-Deeprelay-Error-Code -  <br>  |
| **401** | Missing or invalid API key (OpenAI error envelope). |  * X-Deeprelay-Error-Code -  <br>  |
| **429** | Rate limit or subscription quota exceeded (OpenAI error envelope). A per-key or per-IP rate limit (&#x60;rate_limit_exceeded&#x60;) carries Retry-After, the whole seconds to wait, rounded up (minimum 1), and retry-after-ms, the exact wait; both are the time until one request is allowed, not a full refill. A per-key denial also carries the x-ratelimit-*-requests headers. A subscription quota denial (&#x60;subscription_quota_exhausted&#x60;, raised only when the wallet cannot cover the pay-as-you-go fallback) carries &#x60;x-should-retry: false&#x60; and no Retry-After. When the tripped gate is a rolling 7-day cap (&#x60;param: weekly_input_tokens&#x60; or &#x60;param: weekly_output_tokens&#x60;), the error object also carries &#x60;quota_frees_at&#x60;, the RFC 3339 time the window frees enough capacity — the earlier of the two windows. &#x60;param&#x60; names the tripped gate: monthly_input_tokens, monthly_output_tokens, weekly_input_tokens, weekly_output_tokens, max_usage, input_overshoot (this request\&#39;s estimated input alone exceeds what is left in the tighter of the monthly and rolling 7-day input allowances), or output_overshoot (the same for the estimated output — the completion bound). On an overshoot the quota is not exhausted — send a smaller request (or a smaller max_tokens) or add credits. |  * X-Deeprelay-Requested-Model -  <br>  * X-Deeprelay-Fallback-Attempted -  <br>  * Retry-After - Seconds the client should wait before retrying. <br>  * retry-after-ms -  <br>  * x-ratelimit-limit-requests -  <br>  * x-ratelimit-remaining-requests -  <br>  * x-ratelimit-reset-requests -  <br>  * x-should-retry -  <br>  * X-Deeprelay-Error-Code -  <br>  |
| **500** | Internal server error (OpenAI error envelope). |  * X-Deeprelay-Error-Code -  <br>  |

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


## listFiles

> BatchFileList listFiles(purpose, after, limit, order)

List batch files (OpenAI-compatible)

Lists the organization\&#39;s batch files: inputs you uploaded and the output and error files written for finished batches. Deleted and expired files are not listed.

### Example

```ts
import {
  Configuration,
  BatchApi,
} from '@deeprelay/sdk';
import type { ListFilesRequest } from '@deeprelay/sdk';

async function example() {
  console.log("🚀 Testing @deeprelay/sdk SDK...");
  const config = new Configuration({ 
    // Configure HTTP bearer authorization: bearerAuth
    accessToken: "YOUR BEARER TOKEN",
  });
  const api = new BatchApi(config);

  const body = {
    // 'batch' | 'batch_output' | 'batch_error' (optional)
    purpose: purpose_example,
    // string (optional)
    after: after_example,
    // number (optional)
    limit: 56,
    // 'asc' | 'desc' (optional)
    order: order_example,
  } satisfies ListFilesRequest;

  try {
    const data = await api.listFiles(body);
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
| **purpose** | `batch`, `batch_output`, `batch_error` |  | [Optional] [Defaults to `undefined`] [Enum: batch, batch_output, batch_error] |
| **after** | `string` |  | [Optional] [Defaults to `undefined`] |
| **limit** | `number` |  | [Optional] [Defaults to `undefined`] |
| **order** | `asc`, `desc` |  | [Optional] [Defaults to `undefined`] [Enum: asc, desc] |

### Return type

[**BatchFileList**](BatchFileList.md)

### Authorization

[bearerAuth](../README.md#bearerAuth)

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: `application/json`


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | A page of file objects. |  -  |
| **401** | Missing or invalid API key (OpenAI error envelope). |  * X-Deeprelay-Error-Code -  <br>  |
| **429** | Rate limit or subscription quota exceeded (OpenAI error envelope). A per-key or per-IP rate limit (&#x60;rate_limit_exceeded&#x60;) carries Retry-After, the whole seconds to wait, rounded up (minimum 1), and retry-after-ms, the exact wait; both are the time until one request is allowed, not a full refill. A per-key denial also carries the x-ratelimit-*-requests headers. A subscription quota denial (&#x60;subscription_quota_exhausted&#x60;, raised only when the wallet cannot cover the pay-as-you-go fallback) carries &#x60;x-should-retry: false&#x60; and no Retry-After. When the tripped gate is a rolling 7-day cap (&#x60;param: weekly_input_tokens&#x60; or &#x60;param: weekly_output_tokens&#x60;), the error object also carries &#x60;quota_frees_at&#x60;, the RFC 3339 time the window frees enough capacity — the earlier of the two windows. &#x60;param&#x60; names the tripped gate: monthly_input_tokens, monthly_output_tokens, weekly_input_tokens, weekly_output_tokens, max_usage, input_overshoot (this request\&#39;s estimated input alone exceeds what is left in the tighter of the monthly and rolling 7-day input allowances), or output_overshoot (the same for the estimated output — the completion bound). On an overshoot the quota is not exhausted — send a smaller request (or a smaller max_tokens) or add credits. |  * X-Deeprelay-Requested-Model -  <br>  * X-Deeprelay-Fallback-Attempted -  <br>  * Retry-After - Seconds the client should wait before retrying. <br>  * retry-after-ms -  <br>  * x-ratelimit-limit-requests -  <br>  * x-ratelimit-remaining-requests -  <br>  * x-ratelimit-reset-requests -  <br>  * x-should-retry -  <br>  * X-Deeprelay-Error-Code -  <br>  |
| **500** | Internal server error (OpenAI error envelope). |  * X-Deeprelay-Error-Code -  <br>  |

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


## retrieveBatch

> Batch retrieveBatch(id)

Retrieve a batch (OpenAI-compatible)

### Example

```ts
import {
  Configuration,
  BatchApi,
} from '@deeprelay/sdk';
import type { RetrieveBatchRequest } from '@deeprelay/sdk';

async function example() {
  console.log("🚀 Testing @deeprelay/sdk SDK...");
  const config = new Configuration({ 
    // Configure HTTP bearer authorization: bearerAuth
    accessToken: "YOUR BEARER TOKEN",
  });
  const api = new BatchApi(config);

  const body = {
    // string
    id: id_example,
  } satisfies RetrieveBatchRequest;

  try {
    const data = await api.retrieveBatch(body);
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

[**Batch**](Batch.md)

### Authorization

[bearerAuth](../README.md#bearerAuth)

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: `application/json`


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | The batch object. |  -  |
| **401** | Missing or invalid API key (OpenAI error envelope). |  * X-Deeprelay-Error-Code -  <br>  |
| **404** | Model or resource not found (OpenAI error envelope). |  * X-Deeprelay-Error-Code -  <br>  |
| **429** | Rate limit or subscription quota exceeded (OpenAI error envelope). A per-key or per-IP rate limit (&#x60;rate_limit_exceeded&#x60;) carries Retry-After, the whole seconds to wait, rounded up (minimum 1), and retry-after-ms, the exact wait; both are the time until one request is allowed, not a full refill. A per-key denial also carries the x-ratelimit-*-requests headers. A subscription quota denial (&#x60;subscription_quota_exhausted&#x60;, raised only when the wallet cannot cover the pay-as-you-go fallback) carries &#x60;x-should-retry: false&#x60; and no Retry-After. When the tripped gate is a rolling 7-day cap (&#x60;param: weekly_input_tokens&#x60; or &#x60;param: weekly_output_tokens&#x60;), the error object also carries &#x60;quota_frees_at&#x60;, the RFC 3339 time the window frees enough capacity — the earlier of the two windows. &#x60;param&#x60; names the tripped gate: monthly_input_tokens, monthly_output_tokens, weekly_input_tokens, weekly_output_tokens, max_usage, input_overshoot (this request\&#39;s estimated input alone exceeds what is left in the tighter of the monthly and rolling 7-day input allowances), or output_overshoot (the same for the estimated output — the completion bound). On an overshoot the quota is not exhausted — send a smaller request (or a smaller max_tokens) or add credits. |  * X-Deeprelay-Requested-Model -  <br>  * X-Deeprelay-Fallback-Attempted -  <br>  * Retry-After - Seconds the client should wait before retrying. <br>  * retry-after-ms -  <br>  * x-ratelimit-limit-requests -  <br>  * x-ratelimit-remaining-requests -  <br>  * x-ratelimit-reset-requests -  <br>  * x-should-retry -  <br>  * X-Deeprelay-Error-Code -  <br>  |
| **500** | Internal server error (OpenAI error envelope). |  * X-Deeprelay-Error-Code -  <br>  |

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


## retrieveFile

> BatchFile retrieveFile(id)

Retrieve a batch file (OpenAI-compatible)

### Example

```ts
import {
  Configuration,
  BatchApi,
} from '@deeprelay/sdk';
import type { RetrieveFileRequest } from '@deeprelay/sdk';

async function example() {
  console.log("🚀 Testing @deeprelay/sdk SDK...");
  const config = new Configuration({ 
    // Configure HTTP bearer authorization: bearerAuth
    accessToken: "YOUR BEARER TOKEN",
  });
  const api = new BatchApi(config);

  const body = {
    // string
    id: id_example,
  } satisfies RetrieveFileRequest;

  try {
    const data = await api.retrieveFile(body);
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

[**BatchFile**](BatchFile.md)

### Authorization

[bearerAuth](../README.md#bearerAuth)

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: `application/json`


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | The file object. |  -  |
| **401** | Missing or invalid API key (OpenAI error envelope). |  * X-Deeprelay-Error-Code -  <br>  |
| **404** | Model or resource not found (OpenAI error envelope). |  * X-Deeprelay-Error-Code -  <br>  |
| **429** | Rate limit or subscription quota exceeded (OpenAI error envelope). A per-key or per-IP rate limit (&#x60;rate_limit_exceeded&#x60;) carries Retry-After, the whole seconds to wait, rounded up (minimum 1), and retry-after-ms, the exact wait; both are the time until one request is allowed, not a full refill. A per-key denial also carries the x-ratelimit-*-requests headers. A subscription quota denial (&#x60;subscription_quota_exhausted&#x60;, raised only when the wallet cannot cover the pay-as-you-go fallback) carries &#x60;x-should-retry: false&#x60; and no Retry-After. When the tripped gate is a rolling 7-day cap (&#x60;param: weekly_input_tokens&#x60; or &#x60;param: weekly_output_tokens&#x60;), the error object also carries &#x60;quota_frees_at&#x60;, the RFC 3339 time the window frees enough capacity — the earlier of the two windows. &#x60;param&#x60; names the tripped gate: monthly_input_tokens, monthly_output_tokens, weekly_input_tokens, weekly_output_tokens, max_usage, input_overshoot (this request\&#39;s estimated input alone exceeds what is left in the tighter of the monthly and rolling 7-day input allowances), or output_overshoot (the same for the estimated output — the completion bound). On an overshoot the quota is not exhausted — send a smaller request (or a smaller max_tokens) or add credits. |  * X-Deeprelay-Requested-Model -  <br>  * X-Deeprelay-Fallback-Attempted -  <br>  * Retry-After - Seconds the client should wait before retrying. <br>  * retry-after-ms -  <br>  * x-ratelimit-limit-requests -  <br>  * x-ratelimit-remaining-requests -  <br>  * x-ratelimit-reset-requests -  <br>  * x-should-retry -  <br>  * X-Deeprelay-Error-Code -  <br>  |
| **500** | Internal server error (OpenAI error envelope). |  * X-Deeprelay-Error-Code -  <br>  |

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


## retrieveFileContent

> Blob retrieveFileContent(id)

Download a batch file\&#39;s content (JSONL)

Streams the file\&#39;s JSONL content. For an output or error file each line is a &#x60;BatchResultLine&#x60;. A file past its &#x60;expires_at&#x60; is 410 &#x60;expired&#x60;.

### Example

```ts
import {
  Configuration,
  BatchApi,
} from '@deeprelay/sdk';
import type { RetrieveFileContentRequest } from '@deeprelay/sdk';

async function example() {
  console.log("🚀 Testing @deeprelay/sdk SDK...");
  const config = new Configuration({ 
    // Configure HTTP bearer authorization: bearerAuth
    accessToken: "YOUR BEARER TOKEN",
  });
  const api = new BatchApi(config);

  const body = {
    // string
    id: id_example,
  } satisfies RetrieveFileContentRequest;

  try {
    const data = await api.retrieveFileContent(body);
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

**Blob**

### Authorization

[bearerAuth](../README.md#bearerAuth)

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: `application/jsonl`, `application/json`


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | The file content, one JSON object per line. |  -  |
| **401** | Missing or invalid API key (OpenAI error envelope). |  * X-Deeprelay-Error-Code -  <br>  |
| **404** | Model or resource not found (OpenAI error envelope). |  * X-Deeprelay-Error-Code -  <br>  |
| **410** | The requested artifact has expired and is no longer available (OpenAI error envelope). |  * X-Deeprelay-Error-Code -  <br>  |
| **429** | Rate limit or subscription quota exceeded (OpenAI error envelope). A per-key or per-IP rate limit (&#x60;rate_limit_exceeded&#x60;) carries Retry-After, the whole seconds to wait, rounded up (minimum 1), and retry-after-ms, the exact wait; both are the time until one request is allowed, not a full refill. A per-key denial also carries the x-ratelimit-*-requests headers. A subscription quota denial (&#x60;subscription_quota_exhausted&#x60;, raised only when the wallet cannot cover the pay-as-you-go fallback) carries &#x60;x-should-retry: false&#x60; and no Retry-After. When the tripped gate is a rolling 7-day cap (&#x60;param: weekly_input_tokens&#x60; or &#x60;param: weekly_output_tokens&#x60;), the error object also carries &#x60;quota_frees_at&#x60;, the RFC 3339 time the window frees enough capacity — the earlier of the two windows. &#x60;param&#x60; names the tripped gate: monthly_input_tokens, monthly_output_tokens, weekly_input_tokens, weekly_output_tokens, max_usage, input_overshoot (this request\&#39;s estimated input alone exceeds what is left in the tighter of the monthly and rolling 7-day input allowances), or output_overshoot (the same for the estimated output — the completion bound). On an overshoot the quota is not exhausted — send a smaller request (or a smaller max_tokens) or add credits. |  * X-Deeprelay-Requested-Model -  <br>  * X-Deeprelay-Fallback-Attempted -  <br>  * Retry-After - Seconds the client should wait before retrying. <br>  * retry-after-ms -  <br>  * x-ratelimit-limit-requests -  <br>  * x-ratelimit-remaining-requests -  <br>  * x-ratelimit-reset-requests -  <br>  * x-should-retry -  <br>  * X-Deeprelay-Error-Code -  <br>  |
| **500** | Internal server error (OpenAI error envelope). |  * X-Deeprelay-Error-Code -  <br>  |

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)

