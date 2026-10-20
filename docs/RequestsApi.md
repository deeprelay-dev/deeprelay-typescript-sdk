# RequestsApi

All URIs are relative to *https://api.deeprelay.ai/v1*

| Method | HTTP request | Description |
|------------- | ------------- | -------------|
| [**exportRequests**](RequestsApi.md#exportrequests) | **GET** /requests/export | Export the request log as CSV |
| [**getRequest**](RequestsApi.md#getrequest) | **GET** /requests/{id} | Get one request |
| [**listRequests**](RequestsApi.md#listrequests) | **GET** /requests | List requests (the request log) |



## exportRequests

> string exportRequests(key, model, surface, status, errorCode, clientRequestId, from, to)

Export the request log as CSV

Streams every request-log row matching the filters as a CSV attachment, oldest columns first: &#x60;request_id, client_request_id, occurred_at, surface, model, key_id, key_name, key_prefix, status, http_status, error_code, finish_reason, prompt_tokens, completion_tokens, cached_tokens, reasoning_tokens, quota_units, cost, plan_covered, ttft_ms, duration_ms, ignored_params&#x60;. Takes the same filters and visibility rules as &#x60;GET /requests&#x60;, without the cursor and limit.  The export is counted before anything is written. When the filters match more rows than the export cap, the answer is 422 &#x60;export_too_large&#x60; and the problem body carries &#x60;max_rows&#x60;; narrow the time range or add a filter, then export again.  Requires the &#x60;serverless:read&#x60; scope. Exports have their own, tighter per-key rate limit. 

### Example

```ts
import {
  Configuration,
  RequestsApi,
} from '@deeprelay/sdk';
import type { ExportRequestsRequest } from '@deeprelay/sdk';

async function example() {
  console.log("🚀 Testing @deeprelay/sdk SDK...");
  const config = new Configuration({ 
    // Configure HTTP bearer authorization: bearerAuth
    accessToken: "YOUR BEARER TOKEN",
  });
  const api = new RequestsApi(config);

  const body = {
    // string | Only rows sent with this API key (its `api_key_id`). (optional)
    key: 38400000-8cf0-11bd-b23e-10b96e4ef00d,
    // string | Only rows for this model id. (optional)
    model: model_example,
    // 'chat' | 'messages' | 'responses' | 'embeddings' | 'image' | 'video' | Only rows from this endpoint family. (optional)
    surface: surface_example,
    // 'ok' | 'error' | 'cancelled' | 'rejected' | Only rows with this outcome. `rejected` is a call refused before it reached a model (a budget, limit, allowlist or quota gate). (optional)
    status: status_example,
    // string | Only rows that ended with this `X-Deeprelay-Error-Code`. (optional)
    errorCode: errorCode_example,
    // string | Only rows whose `X-Client-Request-Id` equals this value. (optional)
    clientRequestId: clientRequestId_example,
    // Date | Inclusive RFC 3339 range start. Defaults to the start of the 90-day window; an older value is clamped to it. (optional)
    from: 2013-10-20T19:20:30+01:00,
    // Date | Exclusive RFC 3339 range end. Defaults to now; must be after `from`. (optional)
    to: 2013-10-20T19:20:30+01:00,
  } satisfies ExportRequestsRequest;

  try {
    const data = await api.exportRequests(body);
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
| **key** | `string` | Only rows sent with this API key (its &#x60;api_key_id&#x60;). | [Optional] [Defaults to `undefined`] |
| **model** | `string` | Only rows for this model id. | [Optional] [Defaults to `undefined`] |
| **surface** | `chat`, `messages`, `responses`, `embeddings`, `image`, `video` | Only rows from this endpoint family. | [Optional] [Defaults to `undefined`] [Enum: chat, messages, responses, embeddings, image, video] |
| **status** | `ok`, `error`, `cancelled`, `rejected` | Only rows with this outcome. &#x60;rejected&#x60; is a call refused before it reached a model (a budget, limit, allowlist or quota gate). | [Optional] [Defaults to `undefined`] [Enum: ok, error, cancelled, rejected] |
| **errorCode** | `string` | Only rows that ended with this &#x60;X-Deeprelay-Error-Code&#x60;. | [Optional] [Defaults to `undefined`] |
| **clientRequestId** | `string` | Only rows whose &#x60;X-Client-Request-Id&#x60; equals this value. | [Optional] [Defaults to `undefined`] |
| **from** | `Date` | Inclusive RFC 3339 range start. Defaults to the start of the 90-day window; an older value is clamped to it. | [Optional] [Defaults to `undefined`] |
| **to** | `Date` | Exclusive RFC 3339 range end. Defaults to now; must be after &#x60;from&#x60;. | [Optional] [Defaults to `undefined`] |

### Return type

**string**

### Authorization

[bearerAuth](../README.md#bearerAuth)

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: `text/csv`, `application/problem+json`


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | CSV attachment (&#x60;Content-Disposition&#x60; names the file). |  -  |
| **400** | Error response (RFC 7807) |  -  |
| **422** | &#x60;export_too_large&#x60;: the filters match more rows than the export cap. &#x60;max_rows&#x60; in the problem body is the cap. |  -  |
| **429** | Rate limit exceeded (RFC 7807). Retry-After header indicates seconds to wait. |  * Retry-After - Seconds the client should wait before retrying. <br>  |
| **0** | Error response (RFC 7807) |  -  |

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


## getRequest

> RequestLogEntry getRequest(id)

Get one request

Returns one request-log row. An unknown id, an id older than 90 days and an id the caller cannot see all answer the same 404. Requires the &#x60;serverless:read&#x60; scope. 

### Example

```ts
import {
  Configuration,
  RequestsApi,
} from '@deeprelay/sdk';
import type { GetRequestRequest } from '@deeprelay/sdk';

async function example() {
  console.log("🚀 Testing @deeprelay/sdk SDK...");
  const config = new Configuration({ 
    // Configure HTTP bearer authorization: bearerAuth
    accessToken: "YOUR BEARER TOKEN",
  });
  const api = new RequestsApi(config);

  const body = {
    // string | Any id the caller holds for the request: the `X-Request-Id` response header, a chat completion id (`chatcmpl-…`), a message id (`msg_…`), a response id (`resp_…`) or a video id.
    id: id_example,
  } satisfies GetRequestRequest;

  try {
    const data = await api.getRequest(body);
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
| **id** | `string` | Any id the caller holds for the request: the &#x60;X-Request-Id&#x60; response header, a chat completion id (&#x60;chatcmpl-…&#x60;), a message id (&#x60;msg_…&#x60;), a response id (&#x60;resp_…&#x60;) or a video id. | [Defaults to `undefined`] |

### Return type

[**RequestLogEntry**](RequestLogEntry.md)

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


## listRequests

> RequestLogPage listRequests(key, model, surface, status, errorCode, clientRequestId, from, to, cursor, limit)

List requests (the request log)

Returns one newest-first page of the organization\&#39;s inference request log: one row per call to chat completions, messages, responses, embeddings, image generation or video creation, including calls that were refused before they reached a model (&#x60;status: rejected&#x60;). Rows are kept for 90 days; &#x60;window_days&#x60; says how far back the log reaches, and a &#x60;from&#x60; older than that is clamped rather than rejected.  Visibility follows the caller. An org admin\&#39;s key and a &#x60;full_access&#x60; key see the whole organization; any other key sees only its own rows. A &#x60;key&#x60; filter naming a key the caller cannot see returns an empty page.  A row never carries prompt or completion content. &#x60;client_request_id&#x60; is the value the caller sent in &#x60;X-Client-Request-Id&#x60; (or &#x60;metadata.client_request_id&#x60; on &#x60;/responses&#x60;), kept for correlation.  Requires the &#x60;serverless:read&#x60; scope. Reads are rate-limited per key (429 &#x60;rate_limited&#x60; with Retry-After). 

### Example

```ts
import {
  Configuration,
  RequestsApi,
} from '@deeprelay/sdk';
import type { ListRequestsRequest } from '@deeprelay/sdk';

async function example() {
  console.log("🚀 Testing @deeprelay/sdk SDK...");
  const config = new Configuration({ 
    // Configure HTTP bearer authorization: bearerAuth
    accessToken: "YOUR BEARER TOKEN",
  });
  const api = new RequestsApi(config);

  const body = {
    // string | Only rows sent with this API key (its `api_key_id`). (optional)
    key: 38400000-8cf0-11bd-b23e-10b96e4ef00d,
    // string | Only rows for this model id. (optional)
    model: model_example,
    // 'chat' | 'messages' | 'responses' | 'embeddings' | 'image' | 'video' | Only rows from this endpoint family. (optional)
    surface: surface_example,
    // 'ok' | 'error' | 'cancelled' | 'rejected' | Only rows with this outcome. `rejected` is a call refused before it reached a model (a budget, limit, allowlist or quota gate). (optional)
    status: status_example,
    // string | Only rows that ended with this `X-Deeprelay-Error-Code`. (optional)
    errorCode: errorCode_example,
    // string | Only rows whose `X-Client-Request-Id` equals this value. (optional)
    clientRequestId: clientRequestId_example,
    // Date | Inclusive RFC 3339 range start. Defaults to the start of the 90-day window; an older value is clamped to it. (optional)
    from: 2013-10-20T19:20:30+01:00,
    // Date | Exclusive RFC 3339 range end. Defaults to now; must be after `from`. (optional)
    to: 2013-10-20T19:20:30+01:00,
    // string (optional)
    cursor: cursor_example,
    // number | Page size. Defaults to 50; values above 100 are clamped to 100. (optional)
    limit: 56,
  } satisfies ListRequestsRequest;

  try {
    const data = await api.listRequests(body);
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
| **key** | `string` | Only rows sent with this API key (its &#x60;api_key_id&#x60;). | [Optional] [Defaults to `undefined`] |
| **model** | `string` | Only rows for this model id. | [Optional] [Defaults to `undefined`] |
| **surface** | `chat`, `messages`, `responses`, `embeddings`, `image`, `video` | Only rows from this endpoint family. | [Optional] [Defaults to `undefined`] [Enum: chat, messages, responses, embeddings, image, video] |
| **status** | `ok`, `error`, `cancelled`, `rejected` | Only rows with this outcome. &#x60;rejected&#x60; is a call refused before it reached a model (a budget, limit, allowlist or quota gate). | [Optional] [Defaults to `undefined`] [Enum: ok, error, cancelled, rejected] |
| **errorCode** | `string` | Only rows that ended with this &#x60;X-Deeprelay-Error-Code&#x60;. | [Optional] [Defaults to `undefined`] |
| **clientRequestId** | `string` | Only rows whose &#x60;X-Client-Request-Id&#x60; equals this value. | [Optional] [Defaults to `undefined`] |
| **from** | `Date` | Inclusive RFC 3339 range start. Defaults to the start of the 90-day window; an older value is clamped to it. | [Optional] [Defaults to `undefined`] |
| **to** | `Date` | Exclusive RFC 3339 range end. Defaults to now; must be after &#x60;from&#x60;. | [Optional] [Defaults to `undefined`] |
| **cursor** | `string` |  | [Optional] [Defaults to `undefined`] |
| **limit** | `number` | Page size. Defaults to 50; values above 100 are clamped to 100. | [Optional] [Defaults to `50`] |

### Return type

[**RequestLogPage**](RequestLogPage.md)

### Authorization

[bearerAuth](../README.md#bearerAuth)

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: `application/json`, `application/problem+json`


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | OK |  -  |
| **400** | Error response (RFC 7807) |  -  |
| **429** | Rate limit exceeded (RFC 7807). Retry-After header indicates seconds to wait. |  * Retry-After - Seconds the client should wait before retrying. <br>  |
| **0** | Error response (RFC 7807) |  -  |

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)

