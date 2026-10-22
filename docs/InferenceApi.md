# InferenceApi

All URIs are relative to *https://api.deeprelay.ai/v1*

| Method | HTTP request | Description |
|------------- | ------------- | -------------|
| [**cancelVideo**](InferenceApi.md#cancelvideo) | **POST** /videos/{id}/cancel | Cancel a video generation job |
| [**createChatCompletion**](InferenceApi.md#createchatcompletion) | **POST** /chat/completions | Create a chat completion (OpenAI-compatible) |
| [**createEmbeddings**](InferenceApi.md#createembeddings) | **POST** /embeddings | Create embeddings (OpenAI-compatible) |
| [**createImage**](InferenceApi.md#createimage) | **POST** /images/generations | Create image (OpenAI-compatible) |
| [**createVideo**](InferenceApi.md#createvideo) | **POST** /videos | Create a video generation job (async) |
| [**getModel**](InferenceApi.md#getmodel) | **GET** /models/{id} | Get a specific model (OpenAI-compatible) |
| [**getVideo**](InferenceApi.md#getvideo) | **GET** /videos/{id} | Get a video generation job |
| [**getVideoContent**](InferenceApi.md#getvideocontent) | **GET** /videos/{id}/content | Download a completed video artifact |
| [**inferencePreflight**](InferenceApi.md#inferencepreflight) | **GET** /inference/preflight | Check whether a model request would be served, and at whose expense |
| [**listModels**](InferenceApi.md#listmodels) | **GET** /models | List available models (OpenAI-compatible) |
| [**listVideos**](InferenceApi.md#listvideos) | **GET** /videos | List video generation jobs |



## cancelVideo

> VideoJob cancelVideo(id)

Cancel a video generation job

### Example

```ts
import {
  Configuration,
  InferenceApi,
} from '@deeprelay/sdk';
import type { CancelVideoRequest } from '@deeprelay/sdk';

async function example() {
  console.log("🚀 Testing @deeprelay/sdk SDK...");
  const config = new Configuration({ 
    // Configure HTTP bearer authorization: bearerAuth
    accessToken: "YOUR BEARER TOKEN",
  });
  const api = new InferenceApi(config);

  const body = {
    // string
    id: id_example,
  } satisfies CancelVideoRequest;

  try {
    const data = await api.cancelVideo(body);
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

[**VideoJob**](VideoJob.md)

### Authorization

[bearerAuth](../README.md#bearerAuth)

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: `application/json`


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | A video generation job object. |  -  |
| **401** | Missing or invalid API key (OpenAI error envelope). |  * X-Deeprelay-Error-Code -  <br>  |
| **403** | API key lacks the required scope (&#x60;insufficient_scope&#x60;), or the key has a model allowlist that does not include the requested model (&#x60;model_not_allowed_for_key&#x60;; also the answer for a model that does not exist, so a restricted key cannot probe the catalog). OpenAI error envelope. |  * X-Deeprelay-Error-Code -  <br>  |
| **404** | Model or resource not found (OpenAI error envelope). |  * X-Deeprelay-Error-Code -  <br>  |
| **409** | Invalid request (OpenAI error envelope). |  * X-Deeprelay-Requested-Model -  <br>  * X-Deeprelay-Fallback-Attempted -  <br>  * X-Deeprelay-Error-Code -  <br>  |
| **429** | Rate limit or subscription quota exceeded (OpenAI error envelope). A per-key or per-IP rate limit (&#x60;rate_limit_exceeded&#x60;) carries Retry-After, the whole seconds to wait, rounded up (minimum 1), and retry-after-ms, the exact wait; both are the time until one request is allowed, not a full refill. A per-key denial also carries the x-ratelimit-*-requests headers. A subscription quota denial (&#x60;subscription_quota_exhausted&#x60;, raised only when the wallet cannot cover the pay-as-you-go fallback) carries &#x60;x-should-retry: false&#x60; and no Retry-After. When the tripped gate is a rolling 7-day cap (&#x60;param: weekly_input_tokens&#x60; or &#x60;param: weekly_output_tokens&#x60;), the error object also carries &#x60;quota_frees_at&#x60;, the RFC 3339 time the window frees enough capacity — the earlier of the two windows. &#x60;param&#x60; names the tripped gate: monthly_input_tokens, monthly_output_tokens, weekly_input_tokens, weekly_output_tokens, max_usage, input_overshoot (this request\&#39;s estimated input alone exceeds what is left in the tighter of the monthly and rolling 7-day input allowances), or output_overshoot (the same for the estimated output — the completion bound). On an overshoot the quota is not exhausted — send a smaller request (or a smaller max_tokens) or add credits. |  * X-Deeprelay-Requested-Model -  <br>  * X-Deeprelay-Fallback-Attempted -  <br>  * Retry-After - Seconds the client should wait before retrying. <br>  * retry-after-ms -  <br>  * x-ratelimit-limit-requests -  <br>  * x-ratelimit-remaining-requests -  <br>  * x-ratelimit-reset-requests -  <br>  * x-should-retry -  <br>  * X-Deeprelay-Error-Code -  <br>  |

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


## createChatCompletion

> ChatCompletionResponse createChatCompletion(chatCompletionRequest, xClientRequestId, xDeeprelayFallbackModels)

Create a chat completion (OpenAI-compatible)

OpenAI-compatible chat completion. Parameters fall into three groups:  - **Semantic parameters are gated per model.** &#x60;response_format&#x60;,   &#x60;tools&#x60;/&#x60;tool_choice&#x60;, &#x60;logprobs&#x60;/&#x60;top_logprobs&#x60; and &#x60;image_url&#x60;   content parts are sent only to a model whose &#x60;/v1/models&#x60; entry   lists the capability in &#x60;supported_parameters&#x60; (&#x60;vision&#x60; for   images). A model without it returns 400 &#x60;unsupported_parameter&#x60;   whose message names the models that do support it. When the model   supports the parameter but none of its currently routable upstreams   does, the request fails with 503 &#x60;upstream_unavailable&#x60; rather than   being silently degraded. - **Hints are forwarded or dropped, never rejected.**   &#x60;reasoning_effort&#x60;, &#x60;presence_penalty&#x60;, &#x60;frequency_penalty&#x60;, &#x60;seed&#x60;   and &#x60;parallel_tool_calls&#x60; are forwarded to an upstream that accepts   them and otherwise dropped. Every drop is reported in the   &#x60;x-deeprelay-ignored-params&#x60; response header. - **Rejected everywhere.** &#x60;logit_bias&#x60; and &#x60;function_call&#x60; return   400 &#x60;unsupported_parameter&#x60;; &#x60;input_audio&#x60; and &#x60;file&#x60; content parts   return 400 &#x60;unsupported_content_part&#x60;.  A non-strict &#x60;json_schema&#x60; sent to a model that can only guarantee JSON is served as &#x60;json_object&#x60; and reported as &#x60;response_format:downgraded&#x60;; a strict one is rejected. A &#x60;json_schema&#x60; over 64 KiB or nested deeper than 32 levels returns 400 &#x60;unsupported_parameter&#x60; (param &#x60;response_format&#x60;). An upstream rejection of a request the relay accepted returns 400 &#x60;upstream_rejected_request&#x60;. A non-chat model id returns 404 &#x60;model_not_found&#x60;. The request body is capped at 32 MiB (413 &#x60;request_too_large&#x60;).  Every successful response carries &#x60;usage.cost&#x60; and &#x60;usage.cost_details&#x60; (on a stream, only in the final usage chunk). See https://deeprelay.ai/docs/api/inference#openai-compatibility.  **Backup models.** When the API key has &#x60;fallback_models&#x60;, or the request sends &#x60;models&#x60; or X-Deeprelay-Fallback-Models, and every provider for the requested model fails before the first token with a temporary error (unavailable, timed out, rate limited upstream, or stalled), deeprelay tries the next backup model. It never switches after the first byte, and never on a client error, a quota or budget refusal, or a content-filter result. A backup is billed at its own price under the same billing mode as the requested model. The body &#x60;model&#x60; and X-Deeprelay-Served-Model name the model that served; X-Deeprelay-Requested-Model names the one asked for, and X-Deeprelay-Fallback-Reason says why it was passed over. If no model serves, the response is the requested model\&#39;s own error, with X-Deeprelay-Fallback-Attempted. 

### Example

```ts
import {
  Configuration,
  InferenceApi,
} from '@deeprelay/sdk';
import type { CreateChatCompletionRequest } from '@deeprelay/sdk';

async function example() {
  console.log("🚀 Testing @deeprelay/sdk SDK...");
  const config = new Configuration({ 
    // Configure HTTP bearer authorization: bearerAuth
    accessToken: "YOUR BEARER TOKEN",
  });
  const api = new InferenceApi(config);

  const body = {
    // ChatCompletionRequest
    chatCompletionRequest: ...,
    // string | Your own correlation id for this call, up to 128 characters. It is stored on the request-log row as `client_request_id` and can be filtered on with `GET /requests?client_request_id=`. When it is absent, an inbound `X-Request-Id` is kept in its place; the response\'s own `X-Request-Id` is always minted by deeprelay. Surrounding whitespace and control characters are removed; a longer value is dropped, never truncated. It is never used as a lookup key, so it does not need to be unique. (optional)
    xClientRequestId: xClientRequestId_example,
    // string | Backup models for this request only, in priority order: a comma-separated list of up to 3 model ids, for example `deeprelay/glm-5.3,deeprelay/kimi-k3`. It replaces the API key\'s `fallback_models` for this request; the two lists are never merged. `none` (or an empty value) turns model fallback off for this request. If every provider for the requested model fails before the first token with a temporary error, deeprelay tries the next listed model. Each backup must still pass the key\'s model allowlist, the request\'s billing mode and the request\'s capability needs; one that does not is skipped, so this header can never widen what the key may call. More than 3 models, a malformed id, `none` mixed with ids, or this header together with a `models` body field is a 400 `invalid_request`. Not accepted by Liquid, which always serves exactly the requested model. (optional)
    xDeeprelayFallbackModels: deeprelay/glm-5.3,deeprelay/kimi-k3,
  } satisfies CreateChatCompletionRequest;

  try {
    const data = await api.createChatCompletion(body);
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
| **chatCompletionRequest** | [ChatCompletionRequest](ChatCompletionRequest.md) |  | |
| **xClientRequestId** | `string` | Your own correlation id for this call, up to 128 characters. It is stored on the request-log row as &#x60;client_request_id&#x60; and can be filtered on with &#x60;GET /requests?client_request_id&#x3D;&#x60;. When it is absent, an inbound &#x60;X-Request-Id&#x60; is kept in its place; the response\&#39;s own &#x60;X-Request-Id&#x60; is always minted by deeprelay. Surrounding whitespace and control characters are removed; a longer value is dropped, never truncated. It is never used as a lookup key, so it does not need to be unique. | [Optional] [Defaults to `undefined`] |
| **xDeeprelayFallbackModels** | `string` | Backup models for this request only, in priority order: a comma-separated list of up to 3 model ids, for example &#x60;deeprelay/glm-5.3,deeprelay/kimi-k3&#x60;. It replaces the API key\&#39;s &#x60;fallback_models&#x60; for this request; the two lists are never merged. &#x60;none&#x60; (or an empty value) turns model fallback off for this request. If every provider for the requested model fails before the first token with a temporary error, deeprelay tries the next listed model. Each backup must still pass the key\&#39;s model allowlist, the request\&#39;s billing mode and the request\&#39;s capability needs; one that does not is skipped, so this header can never widen what the key may call. More than 3 models, a malformed id, &#x60;none&#x60; mixed with ids, or this header together with a &#x60;models&#x60; body field is a 400 &#x60;invalid_request&#x60;. Not accepted by Liquid, which always serves exactly the requested model. | [Optional] [Defaults to `undefined`] |

### Return type

[**ChatCompletionResponse**](ChatCompletionResponse.md)

### Authorization

[bearerAuth](../README.md#bearerAuth)

### HTTP request headers

- **Content-Type**: `application/json`
- **Accept**: `application/json`, `text/event-stream`


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | Successful response. application/json for non-streaming requests; text/event-stream for streaming requests (stream&#x3D;true).  |  * X-Deeprelay-Served-Model -  <br>  * X-Deeprelay-Requested-Model -  <br>  * X-Deeprelay-Fallback-Reason -  <br>  * x-deeprelay-ignored-params -  <br>  * x-deeprelay-cost -  <br>  * x-deeprelay-quota-input-remaining -  <br>  * x-deeprelay-quota-output-remaining -  <br>  * x-deeprelay-quota-reset -  <br>  * x-deeprelay-quota-weekly-input-remaining -  <br>  * x-deeprelay-quota-weekly-input-limit -  <br>  * x-deeprelay-quota-weekly-output-remaining -  <br>  * x-deeprelay-quota-weekly-output-limit -  <br>  * x-ratelimit-limit-requests -  <br>  * x-ratelimit-remaining-requests -  <br>  * x-ratelimit-reset-requests -  <br>  |
| **400** | Invalid request (OpenAI error envelope). |  * X-Deeprelay-Requested-Model -  <br>  * X-Deeprelay-Fallback-Attempted -  <br>  * X-Deeprelay-Error-Code -  <br>  |
| **401** | Missing or invalid API key (OpenAI error envelope). |  * X-Deeprelay-Error-Code -  <br>  |
| **402** | Insufficient balance or a spend limit reached (OpenAI error envelope, SERV-06): &#x60;insufficient_balance&#x60;, &#x60;daily_limit_reached&#x60;, &#x60;spending_limit_reached&#x60;, &#x60;api_key_budget_exceeded&#x60; (this API key\&#39;s monthly budget) or &#x60;member_spend_limit_reached&#x60; (the member\&#39;s monthly spend limit). Carries &#x60;x-should-retry: false&#x60;: the same request will not succeed until the wallet or the limit changes. |  * x-should-retry -  <br>  * X-Deeprelay-Error-Code -  <br>  |
| **403** | API key lacks the required scope (&#x60;insufficient_scope&#x60;), or the key has a model allowlist that does not include the requested model (&#x60;model_not_allowed_for_key&#x60;; also the answer for a model that does not exist, so a restricted key cannot probe the catalog). OpenAI error envelope. |  * X-Deeprelay-Error-Code -  <br>  |
| **404** | Model or resource not found (OpenAI error envelope). |  * X-Deeprelay-Error-Code -  <br>  |
| **413** | Request body too large (OpenAI error envelope, code request_too_large). |  * X-Deeprelay-Error-Code -  <br>  |
| **422** | Request validation failed (OpenAI error envelope). |  * X-Deeprelay-Error-Code -  <br>  |
| **429** | Rate limit or subscription quota exceeded (OpenAI error envelope). A per-key or per-IP rate limit (&#x60;rate_limit_exceeded&#x60;) carries Retry-After, the whole seconds to wait, rounded up (minimum 1), and retry-after-ms, the exact wait; both are the time until one request is allowed, not a full refill. A per-key denial also carries the x-ratelimit-*-requests headers. A subscription quota denial (&#x60;subscription_quota_exhausted&#x60;, raised only when the wallet cannot cover the pay-as-you-go fallback) carries &#x60;x-should-retry: false&#x60; and no Retry-After. When the tripped gate is a rolling 7-day cap (&#x60;param: weekly_input_tokens&#x60; or &#x60;param: weekly_output_tokens&#x60;), the error object also carries &#x60;quota_frees_at&#x60;, the RFC 3339 time the window frees enough capacity — the earlier of the two windows. &#x60;param&#x60; names the tripped gate: monthly_input_tokens, monthly_output_tokens, weekly_input_tokens, weekly_output_tokens, max_usage, input_overshoot (this request\&#39;s estimated input alone exceeds what is left in the tighter of the monthly and rolling 7-day input allowances), or output_overshoot (the same for the estimated output — the completion bound). On an overshoot the quota is not exhausted — send a smaller request (or a smaller max_tokens) or add credits. |  * X-Deeprelay-Requested-Model -  <br>  * X-Deeprelay-Fallback-Attempted -  <br>  * Retry-After - Seconds the client should wait before retrying. <br>  * retry-after-ms -  <br>  * x-ratelimit-limit-requests -  <br>  * x-ratelimit-remaining-requests -  <br>  * x-ratelimit-reset-requests -  <br>  * x-should-retry -  <br>  * X-Deeprelay-Error-Code -  <br>  |
| **500** | Internal server error (OpenAI error envelope). |  * X-Deeprelay-Error-Code -  <br>  |
| **503** | No upstream could serve the request (OpenAI error envelope, &#x60;upstream_unavailable&#x60;): every capable upstream is down, shedding load, or none of the model\&#39;s routable upstreams supports a capability the request needs. Always carries Retry-After (whole seconds, rounded up) and retry-after-ms; on an overload the wait is jittered between 2 and 2.5 seconds. |  * X-Deeprelay-Requested-Model -  <br>  * X-Deeprelay-Fallback-Attempted -  <br>  * Retry-After - Seconds the client should wait before retrying. <br>  * retry-after-ms -  <br>  * X-Deeprelay-Error-Code -  <br>  |

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


## createEmbeddings

> EmbeddingsResponse createEmbeddings(embeddingsRequest, xClientRequestId)

Create embeddings (OpenAI-compatible)

Synchronous text embeddings. Accepts a single string or an array of up to 2048 strings, bounded so the response stays under 64 MiB (about 680 inputs at 4096 dimensions; fewer at a larger &#x60;dimensions&#x60; value) — over-limit requests are rejected with 400 before any processing. Returns one float vector per input, in request order. Billed on the upstream\&#39;s reported prompt tokens at the model\&#39;s listed input rate, rounded up to the next whole cent per request; an embeddings call emits no completion tokens, so &#x60;usage&#x60; carries &#x60;prompt_tokens&#x60; and &#x60;total_tokens&#x60; only. &#x60;encoding_format&#x60; accepts only &#x60;float&#x60; — a value of &#x60;base64&#x60; is rejected with &#x60;unsupported_parameter&#x60;. A chat model id on this route returns 404 &#x60;model_not_found&#x60;: the id is valid, but not on this surface.

### Example

```ts
import {
  Configuration,
  InferenceApi,
} from '@deeprelay/sdk';
import type { CreateEmbeddingsRequest } from '@deeprelay/sdk';

async function example() {
  console.log("🚀 Testing @deeprelay/sdk SDK...");
  const config = new Configuration({ 
    // Configure HTTP bearer authorization: bearerAuth
    accessToken: "YOUR BEARER TOKEN",
  });
  const api = new InferenceApi(config);

  const body = {
    // EmbeddingsRequest
    embeddingsRequest: ...,
    // string | Your own correlation id for this call, up to 128 characters. It is stored on the request-log row as `client_request_id` and can be filtered on with `GET /requests?client_request_id=`. When it is absent, an inbound `X-Request-Id` is kept in its place; the response\'s own `X-Request-Id` is always minted by deeprelay. Surrounding whitespace and control characters are removed; a longer value is dropped, never truncated. It is never used as a lookup key, so it does not need to be unique. (optional)
    xClientRequestId: xClientRequestId_example,
  } satisfies CreateEmbeddingsRequest;

  try {
    const data = await api.createEmbeddings(body);
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
| **embeddingsRequest** | [EmbeddingsRequest](EmbeddingsRequest.md) |  | |
| **xClientRequestId** | `string` | Your own correlation id for this call, up to 128 characters. It is stored on the request-log row as &#x60;client_request_id&#x60; and can be filtered on with &#x60;GET /requests?client_request_id&#x3D;&#x60;. When it is absent, an inbound &#x60;X-Request-Id&#x60; is kept in its place; the response\&#39;s own &#x60;X-Request-Id&#x60; is always minted by deeprelay. Surrounding whitespace and control characters are removed; a longer value is dropped, never truncated. It is never used as a lookup key, so it does not need to be unique. | [Optional] [Defaults to `undefined`] |

### Return type

[**EmbeddingsResponse**](EmbeddingsResponse.md)

### Authorization

[bearerAuth](../README.md#bearerAuth)

### HTTP request headers

- **Content-Type**: `application/json`
- **Accept**: `application/json`


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | One embedding vector per input, in request order. |  -  |
| **400** | Invalid request (OpenAI error envelope). |  * X-Deeprelay-Requested-Model -  <br>  * X-Deeprelay-Fallback-Attempted -  <br>  * X-Deeprelay-Error-Code -  <br>  |
| **401** | Missing or invalid API key (OpenAI error envelope). |  * X-Deeprelay-Error-Code -  <br>  |
| **402** | Insufficient balance or a spend limit reached (OpenAI error envelope, SERV-06): &#x60;insufficient_balance&#x60;, &#x60;daily_limit_reached&#x60;, &#x60;spending_limit_reached&#x60;, &#x60;api_key_budget_exceeded&#x60; (this API key\&#39;s monthly budget) or &#x60;member_spend_limit_reached&#x60; (the member\&#39;s monthly spend limit). Carries &#x60;x-should-retry: false&#x60;: the same request will not succeed until the wallet or the limit changes. |  * x-should-retry -  <br>  * X-Deeprelay-Error-Code -  <br>  |
| **403** | API key lacks the required scope (&#x60;insufficient_scope&#x60;), or the key has a model allowlist that does not include the requested model (&#x60;model_not_allowed_for_key&#x60;; also the answer for a model that does not exist, so a restricted key cannot probe the catalog). OpenAI error envelope. |  * X-Deeprelay-Error-Code -  <br>  |
| **404** | Model or resource not found (OpenAI error envelope). |  * X-Deeprelay-Error-Code -  <br>  |
| **413** | Request body too large (OpenAI error envelope, code request_too_large). |  * X-Deeprelay-Error-Code -  <br>  |
| **429** | Rate limit or subscription quota exceeded (OpenAI error envelope). A per-key or per-IP rate limit (&#x60;rate_limit_exceeded&#x60;) carries Retry-After, the whole seconds to wait, rounded up (minimum 1), and retry-after-ms, the exact wait; both are the time until one request is allowed, not a full refill. A per-key denial also carries the x-ratelimit-*-requests headers. A subscription quota denial (&#x60;subscription_quota_exhausted&#x60;, raised only when the wallet cannot cover the pay-as-you-go fallback) carries &#x60;x-should-retry: false&#x60; and no Retry-After. When the tripped gate is a rolling 7-day cap (&#x60;param: weekly_input_tokens&#x60; or &#x60;param: weekly_output_tokens&#x60;), the error object also carries &#x60;quota_frees_at&#x60;, the RFC 3339 time the window frees enough capacity — the earlier of the two windows. &#x60;param&#x60; names the tripped gate: monthly_input_tokens, monthly_output_tokens, weekly_input_tokens, weekly_output_tokens, max_usage, input_overshoot (this request\&#39;s estimated input alone exceeds what is left in the tighter of the monthly and rolling 7-day input allowances), or output_overshoot (the same for the estimated output — the completion bound). On an overshoot the quota is not exhausted — send a smaller request (or a smaller max_tokens) or add credits. |  * X-Deeprelay-Requested-Model -  <br>  * X-Deeprelay-Fallback-Attempted -  <br>  * Retry-After - Seconds the client should wait before retrying. <br>  * retry-after-ms -  <br>  * x-ratelimit-limit-requests -  <br>  * x-ratelimit-remaining-requests -  <br>  * x-ratelimit-reset-requests -  <br>  * x-should-retry -  <br>  * X-Deeprelay-Error-Code -  <br>  |
| **500** | Internal server error (OpenAI error envelope). |  * X-Deeprelay-Error-Code -  <br>  |
| **502** | The upstream answered but its response could not be used (OpenAI error envelope): code upstream_response_too_large when the vector payload exceeded the per-request size limit, or upstream_error for a malformed / misaligned response. Not retryable as-is for upstream_response_too_large — send fewer inputs. |  * X-Deeprelay-Requested-Model -  <br>  * X-Deeprelay-Fallback-Attempted -  <br>  * X-Deeprelay-Error-Code -  <br>  |
| **503** | No upstream could serve the request (OpenAI error envelope, &#x60;upstream_unavailable&#x60;): every capable upstream is down, shedding load, or none of the model\&#39;s routable upstreams supports a capability the request needs. Always carries Retry-After (whole seconds, rounded up) and retry-after-ms; on an overload the wait is jittered between 2 and 2.5 seconds. |  * X-Deeprelay-Requested-Model -  <br>  * X-Deeprelay-Fallback-Attempted -  <br>  * Retry-After - Seconds the client should wait before retrying. <br>  * retry-after-ms -  <br>  * X-Deeprelay-Error-Code -  <br>  |
| **504** | Upstream provider exceeded the synchronous per-attempt deadline (OpenAI error envelope). 504 semantic — distinct from 503 OpenAIUpstreamUnavailable which signals a connection or routing failure rather than a timeout.  |  * X-Deeprelay-Requested-Model -  <br>  * X-Deeprelay-Fallback-Attempted -  <br>  * X-Deeprelay-Error-Code -  <br>  |

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


## createImage

> ImagesResponse createImage(imagesGenerationsRequest, idempotencyKey, xClientRequestId)

Create image (OpenAI-compatible)

Synchronous text-to-image generation. Returns base64-encoded images only (&#x60;response_format&#x60; is restricted to &#x60;b64_json&#x60;); a value of &#x60;url&#x60; is rejected with &#x60;invalid_request_error&#x60; until S3-backed URL delivery lands. Pass an &#x60;Idempotency-Key&#x60; header to make a retried request replay the original response without a second charge.

### Example

```ts
import {
  Configuration,
  InferenceApi,
} from '@deeprelay/sdk';
import type { CreateImageRequest } from '@deeprelay/sdk';

async function example() {
  console.log("🚀 Testing @deeprelay/sdk SDK...");
  const config = new Configuration({ 
    // Configure HTTP bearer authorization: bearerAuth
    accessToken: "YOUR BEARER TOKEN",
  });
  const api = new InferenceApi(config);

  const body = {
    // ImagesGenerationsRequest
    imagesGenerationsRequest: ...,
    // string (optional)
    idempotencyKey: idempotencyKey_example,
    // string | Your own correlation id for this call, up to 128 characters. It is stored on the request-log row as `client_request_id` and can be filtered on with `GET /requests?client_request_id=`. When it is absent, an inbound `X-Request-Id` is kept in its place; the response\'s own `X-Request-Id` is always minted by deeprelay. Surrounding whitespace and control characters are removed; a longer value is dropped, never truncated. It is never used as a lookup key, so it does not need to be unique. (optional)
    xClientRequestId: xClientRequestId_example,
  } satisfies CreateImageRequest;

  try {
    const data = await api.createImage(body);
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
| **imagesGenerationsRequest** | [ImagesGenerationsRequest](ImagesGenerationsRequest.md) |  | |
| **idempotencyKey** | `string` |  | [Optional] [Defaults to `undefined`] |
| **xClientRequestId** | `string` | Your own correlation id for this call, up to 128 characters. It is stored on the request-log row as &#x60;client_request_id&#x60; and can be filtered on with &#x60;GET /requests?client_request_id&#x3D;&#x60;. When it is absent, an inbound &#x60;X-Request-Id&#x60; is kept in its place; the response\&#39;s own &#x60;X-Request-Id&#x60; is always minted by deeprelay. Surrounding whitespace and control characters are removed; a longer value is dropped, never truncated. It is never used as a lookup key, so it does not need to be unique. | [Optional] [Defaults to `undefined`] |

### Return type

[**ImagesResponse**](ImagesResponse.md)

### Authorization

[bearerAuth](../README.md#bearerAuth)

### HTTP request headers

- **Content-Type**: `application/json`
- **Accept**: `application/json`


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | OpenAI-shaped image generation response (b64_json only). |  -  |
| **400** | Invalid request (OpenAI error envelope). |  * X-Deeprelay-Requested-Model -  <br>  * X-Deeprelay-Fallback-Attempted -  <br>  * X-Deeprelay-Error-Code -  <br>  |
| **401** | Missing or invalid API key (OpenAI error envelope). |  * X-Deeprelay-Error-Code -  <br>  |
| **402** | Insufficient balance or a spend limit reached (OpenAI error envelope, SERV-06): &#x60;insufficient_balance&#x60;, &#x60;daily_limit_reached&#x60;, &#x60;spending_limit_reached&#x60;, &#x60;api_key_budget_exceeded&#x60; (this API key\&#39;s monthly budget) or &#x60;member_spend_limit_reached&#x60; (the member\&#39;s monthly spend limit). Carries &#x60;x-should-retry: false&#x60;: the same request will not succeed until the wallet or the limit changes. |  * x-should-retry -  <br>  * X-Deeprelay-Error-Code -  <br>  |
| **403** | API key lacks the required scope (&#x60;insufficient_scope&#x60;), or the key has a model allowlist that does not include the requested model (&#x60;model_not_allowed_for_key&#x60;; also the answer for a model that does not exist, so a restricted key cannot probe the catalog). OpenAI error envelope. |  * X-Deeprelay-Error-Code -  <br>  |
| **404** | Model or resource not found (OpenAI error envelope). |  * X-Deeprelay-Error-Code -  <br>  |
| **422** | Request validation failed (OpenAI error envelope). |  * X-Deeprelay-Error-Code -  <br>  |
| **429** | Rate limit or subscription quota exceeded (OpenAI error envelope). A per-key or per-IP rate limit (&#x60;rate_limit_exceeded&#x60;) carries Retry-After, the whole seconds to wait, rounded up (minimum 1), and retry-after-ms, the exact wait; both are the time until one request is allowed, not a full refill. A per-key denial also carries the x-ratelimit-*-requests headers. A subscription quota denial (&#x60;subscription_quota_exhausted&#x60;, raised only when the wallet cannot cover the pay-as-you-go fallback) carries &#x60;x-should-retry: false&#x60; and no Retry-After. When the tripped gate is a rolling 7-day cap (&#x60;param: weekly_input_tokens&#x60; or &#x60;param: weekly_output_tokens&#x60;), the error object also carries &#x60;quota_frees_at&#x60;, the RFC 3339 time the window frees enough capacity — the earlier of the two windows. &#x60;param&#x60; names the tripped gate: monthly_input_tokens, monthly_output_tokens, weekly_input_tokens, weekly_output_tokens, max_usage, input_overshoot (this request\&#39;s estimated input alone exceeds what is left in the tighter of the monthly and rolling 7-day input allowances), or output_overshoot (the same for the estimated output — the completion bound). On an overshoot the quota is not exhausted — send a smaller request (or a smaller max_tokens) or add credits. |  * X-Deeprelay-Requested-Model -  <br>  * X-Deeprelay-Fallback-Attempted -  <br>  * Retry-After - Seconds the client should wait before retrying. <br>  * retry-after-ms -  <br>  * x-ratelimit-limit-requests -  <br>  * x-ratelimit-remaining-requests -  <br>  * x-ratelimit-reset-requests -  <br>  * x-should-retry -  <br>  * X-Deeprelay-Error-Code -  <br>  |
| **500** | Internal server error (OpenAI error envelope). |  * X-Deeprelay-Error-Code -  <br>  |
| **503** | No upstream could serve the request (OpenAI error envelope, &#x60;upstream_unavailable&#x60;): every capable upstream is down, shedding load, or none of the model\&#39;s routable upstreams supports a capability the request needs. Always carries Retry-After (whole seconds, rounded up) and retry-after-ms; on an overload the wait is jittered between 2 and 2.5 seconds. |  * X-Deeprelay-Requested-Model -  <br>  * X-Deeprelay-Fallback-Attempted -  <br>  * Retry-After - Seconds the client should wait before retrying. <br>  * retry-after-ms -  <br>  * X-Deeprelay-Error-Code -  <br>  |
| **504** | Upstream provider exceeded the synchronous per-attempt deadline (OpenAI error envelope). 504 semantic — distinct from 503 OpenAIUpstreamUnavailable which signals a connection or routing failure rather than a timeout.  |  * X-Deeprelay-Requested-Model -  <br>  * X-Deeprelay-Fallback-Attempted -  <br>  * X-Deeprelay-Error-Code -  <br>  |

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


## createVideo

> VideoJob createVideo(videoCreateRequest, idempotencyKey, xClientRequestId)

Create a video generation job (async)

Submit an asynchronous text-to-video generation job. Returns a job object with status &#x60;queued&#x60;; poll GET /videos/{id} until &#x60;completed&#x60;, then stream the result from GET /videos/{id}/content. Pass an &#x60;Idempotency-Key&#x60; header to make a retried request replay the original response without a second charge.

### Example

```ts
import {
  Configuration,
  InferenceApi,
} from '@deeprelay/sdk';
import type { CreateVideoRequest } from '@deeprelay/sdk';

async function example() {
  console.log("🚀 Testing @deeprelay/sdk SDK...");
  const config = new Configuration({ 
    // Configure HTTP bearer authorization: bearerAuth
    accessToken: "YOUR BEARER TOKEN",
  });
  const api = new InferenceApi(config);

  const body = {
    // VideoCreateRequest
    videoCreateRequest: ...,
    // string (optional)
    idempotencyKey: idempotencyKey_example,
    // string | Your own correlation id for this call, up to 128 characters. It is stored on the request-log row as `client_request_id` and can be filtered on with `GET /requests?client_request_id=`. When it is absent, an inbound `X-Request-Id` is kept in its place; the response\'s own `X-Request-Id` is always minted by deeprelay. Surrounding whitespace and control characters are removed; a longer value is dropped, never truncated. It is never used as a lookup key, so it does not need to be unique. (optional)
    xClientRequestId: xClientRequestId_example,
  } satisfies CreateVideoRequest;

  try {
    const data = await api.createVideo(body);
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
| **videoCreateRequest** | [VideoCreateRequest](VideoCreateRequest.md) |  | |
| **idempotencyKey** | `string` |  | [Optional] [Defaults to `undefined`] |
| **xClientRequestId** | `string` | Your own correlation id for this call, up to 128 characters. It is stored on the request-log row as &#x60;client_request_id&#x60; and can be filtered on with &#x60;GET /requests?client_request_id&#x3D;&#x60;. When it is absent, an inbound &#x60;X-Request-Id&#x60; is kept in its place; the response\&#39;s own &#x60;X-Request-Id&#x60; is always minted by deeprelay. Surrounding whitespace and control characters are removed; a longer value is dropped, never truncated. It is never used as a lookup key, so it does not need to be unique. | [Optional] [Defaults to `undefined`] |

### Return type

[**VideoJob**](VideoJob.md)

### Authorization

[bearerAuth](../README.md#bearerAuth)

### HTTP request headers

- **Content-Type**: `application/json`
- **Accept**: `application/json`


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | A video generation job object. |  -  |
| **400** | Invalid request (OpenAI error envelope). |  * X-Deeprelay-Requested-Model -  <br>  * X-Deeprelay-Fallback-Attempted -  <br>  * X-Deeprelay-Error-Code -  <br>  |
| **401** | Missing or invalid API key (OpenAI error envelope). |  * X-Deeprelay-Error-Code -  <br>  |
| **402** | Insufficient balance or a spend limit reached (OpenAI error envelope, SERV-06): &#x60;insufficient_balance&#x60;, &#x60;daily_limit_reached&#x60;, &#x60;spending_limit_reached&#x60;, &#x60;api_key_budget_exceeded&#x60; (this API key\&#39;s monthly budget) or &#x60;member_spend_limit_reached&#x60; (the member\&#39;s monthly spend limit). Carries &#x60;x-should-retry: false&#x60;: the same request will not succeed until the wallet or the limit changes. |  * x-should-retry -  <br>  * X-Deeprelay-Error-Code -  <br>  |
| **403** | API key lacks the required scope (&#x60;insufficient_scope&#x60;), or the key has a model allowlist that does not include the requested model (&#x60;model_not_allowed_for_key&#x60;; also the answer for a model that does not exist, so a restricted key cannot probe the catalog). OpenAI error envelope. |  * X-Deeprelay-Error-Code -  <br>  |
| **404** | Model or resource not found (OpenAI error envelope). |  * X-Deeprelay-Error-Code -  <br>  |
| **429** | Rate limit or subscription quota exceeded (OpenAI error envelope). A per-key or per-IP rate limit (&#x60;rate_limit_exceeded&#x60;) carries Retry-After, the whole seconds to wait, rounded up (minimum 1), and retry-after-ms, the exact wait; both are the time until one request is allowed, not a full refill. A per-key denial also carries the x-ratelimit-*-requests headers. A subscription quota denial (&#x60;subscription_quota_exhausted&#x60;, raised only when the wallet cannot cover the pay-as-you-go fallback) carries &#x60;x-should-retry: false&#x60; and no Retry-After. When the tripped gate is a rolling 7-day cap (&#x60;param: weekly_input_tokens&#x60; or &#x60;param: weekly_output_tokens&#x60;), the error object also carries &#x60;quota_frees_at&#x60;, the RFC 3339 time the window frees enough capacity — the earlier of the two windows. &#x60;param&#x60; names the tripped gate: monthly_input_tokens, monthly_output_tokens, weekly_input_tokens, weekly_output_tokens, max_usage, input_overshoot (this request\&#39;s estimated input alone exceeds what is left in the tighter of the monthly and rolling 7-day input allowances), or output_overshoot (the same for the estimated output — the completion bound). On an overshoot the quota is not exhausted — send a smaller request (or a smaller max_tokens) or add credits. |  * X-Deeprelay-Requested-Model -  <br>  * X-Deeprelay-Fallback-Attempted -  <br>  * Retry-After - Seconds the client should wait before retrying. <br>  * retry-after-ms -  <br>  * x-ratelimit-limit-requests -  <br>  * x-ratelimit-remaining-requests -  <br>  * x-ratelimit-reset-requests -  <br>  * x-should-retry -  <br>  * X-Deeprelay-Error-Code -  <br>  |
| **500** | Internal server error (OpenAI error envelope). |  * X-Deeprelay-Error-Code -  <br>  |

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


## getModel

> Model getModel(id)

Get a specific model (OpenAI-compatible)

A key with a model allowlist gets 403 &#x60;model_not_allowed_for_key&#x60; for a model off its list, and the same 403 for an id that does not exist.

### Example

```ts
import {
  Configuration,
  InferenceApi,
} from '@deeprelay/sdk';
import type { GetModelRequest } from '@deeprelay/sdk';

async function example() {
  console.log("🚀 Testing @deeprelay/sdk SDK...");
  const config = new Configuration({ 
    // Configure HTTP bearer authorization: bearerAuth
    accessToken: "YOUR BEARER TOKEN",
  });
  const api = new InferenceApi(config);

  const body = {
    // string
    id: id_example,
  } satisfies GetModelRequest;

  try {
    const data = await api.getModel(body);
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

[**Model**](Model.md)

### Authorization

[bearerAuth](../README.md#bearerAuth)

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: `application/json`


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | OpenAI-shaped single model. |  -  |
| **401** | Missing or invalid API key (OpenAI error envelope). |  * X-Deeprelay-Error-Code -  <br>  |
| **403** | API key lacks the required scope (&#x60;insufficient_scope&#x60;), or the key has a model allowlist that does not include the requested model (&#x60;model_not_allowed_for_key&#x60;; also the answer for a model that does not exist, so a restricted key cannot probe the catalog). OpenAI error envelope. |  * X-Deeprelay-Error-Code -  <br>  |
| **404** | Model or resource not found (OpenAI error envelope). |  * X-Deeprelay-Error-Code -  <br>  |
| **429** | Rate limit or subscription quota exceeded (OpenAI error envelope). A per-key or per-IP rate limit (&#x60;rate_limit_exceeded&#x60;) carries Retry-After, the whole seconds to wait, rounded up (minimum 1), and retry-after-ms, the exact wait; both are the time until one request is allowed, not a full refill. A per-key denial also carries the x-ratelimit-*-requests headers. A subscription quota denial (&#x60;subscription_quota_exhausted&#x60;, raised only when the wallet cannot cover the pay-as-you-go fallback) carries &#x60;x-should-retry: false&#x60; and no Retry-After. When the tripped gate is a rolling 7-day cap (&#x60;param: weekly_input_tokens&#x60; or &#x60;param: weekly_output_tokens&#x60;), the error object also carries &#x60;quota_frees_at&#x60;, the RFC 3339 time the window frees enough capacity — the earlier of the two windows. &#x60;param&#x60; names the tripped gate: monthly_input_tokens, monthly_output_tokens, weekly_input_tokens, weekly_output_tokens, max_usage, input_overshoot (this request\&#39;s estimated input alone exceeds what is left in the tighter of the monthly and rolling 7-day input allowances), or output_overshoot (the same for the estimated output — the completion bound). On an overshoot the quota is not exhausted — send a smaller request (or a smaller max_tokens) or add credits. |  * X-Deeprelay-Requested-Model -  <br>  * X-Deeprelay-Fallback-Attempted -  <br>  * Retry-After - Seconds the client should wait before retrying. <br>  * retry-after-ms -  <br>  * x-ratelimit-limit-requests -  <br>  * x-ratelimit-remaining-requests -  <br>  * x-ratelimit-reset-requests -  <br>  * x-should-retry -  <br>  * X-Deeprelay-Error-Code -  <br>  |

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


## getVideo

> VideoJob getVideo(id)

Get a video generation job

### Example

```ts
import {
  Configuration,
  InferenceApi,
} from '@deeprelay/sdk';
import type { GetVideoRequest } from '@deeprelay/sdk';

async function example() {
  console.log("🚀 Testing @deeprelay/sdk SDK...");
  const config = new Configuration({ 
    // Configure HTTP bearer authorization: bearerAuth
    accessToken: "YOUR BEARER TOKEN",
  });
  const api = new InferenceApi(config);

  const body = {
    // string
    id: id_example,
  } satisfies GetVideoRequest;

  try {
    const data = await api.getVideo(body);
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

[**VideoJob**](VideoJob.md)

### Authorization

[bearerAuth](../README.md#bearerAuth)

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: `application/json`


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | A video generation job object. |  -  |
| **401** | Missing or invalid API key (OpenAI error envelope). |  * X-Deeprelay-Error-Code -  <br>  |
| **403** | API key lacks the required scope (&#x60;insufficient_scope&#x60;), or the key has a model allowlist that does not include the requested model (&#x60;model_not_allowed_for_key&#x60;; also the answer for a model that does not exist, so a restricted key cannot probe the catalog). OpenAI error envelope. |  * X-Deeprelay-Error-Code -  <br>  |
| **404** | Model or resource not found (OpenAI error envelope). |  * X-Deeprelay-Error-Code -  <br>  |
| **429** | Rate limit or subscription quota exceeded (OpenAI error envelope). A per-key or per-IP rate limit (&#x60;rate_limit_exceeded&#x60;) carries Retry-After, the whole seconds to wait, rounded up (minimum 1), and retry-after-ms, the exact wait; both are the time until one request is allowed, not a full refill. A per-key denial also carries the x-ratelimit-*-requests headers. A subscription quota denial (&#x60;subscription_quota_exhausted&#x60;, raised only when the wallet cannot cover the pay-as-you-go fallback) carries &#x60;x-should-retry: false&#x60; and no Retry-After. When the tripped gate is a rolling 7-day cap (&#x60;param: weekly_input_tokens&#x60; or &#x60;param: weekly_output_tokens&#x60;), the error object also carries &#x60;quota_frees_at&#x60;, the RFC 3339 time the window frees enough capacity — the earlier of the two windows. &#x60;param&#x60; names the tripped gate: monthly_input_tokens, monthly_output_tokens, weekly_input_tokens, weekly_output_tokens, max_usage, input_overshoot (this request\&#39;s estimated input alone exceeds what is left in the tighter of the monthly and rolling 7-day input allowances), or output_overshoot (the same for the estimated output — the completion bound). On an overshoot the quota is not exhausted — send a smaller request (or a smaller max_tokens) or add credits. |  * X-Deeprelay-Requested-Model -  <br>  * X-Deeprelay-Fallback-Attempted -  <br>  * Retry-After - Seconds the client should wait before retrying. <br>  * retry-after-ms -  <br>  * x-ratelimit-limit-requests -  <br>  * x-ratelimit-remaining-requests -  <br>  * x-ratelimit-reset-requests -  <br>  * x-should-retry -  <br>  * X-Deeprelay-Error-Code -  <br>  |

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


## getVideoContent

> Blob getVideoContent(id)

Download a completed video artifact

Streams the generated MP4 for a completed job. Returns 410 Gone once the artifact has expired (24h retention).

### Example

```ts
import {
  Configuration,
  InferenceApi,
} from '@deeprelay/sdk';
import type { GetVideoContentRequest } from '@deeprelay/sdk';

async function example() {
  console.log("🚀 Testing @deeprelay/sdk SDK...");
  const config = new Configuration({ 
    // Configure HTTP bearer authorization: bearerAuth
    accessToken: "YOUR BEARER TOKEN",
  });
  const api = new InferenceApi(config);

  const body = {
    // string
    id: id_example,
  } satisfies GetVideoContentRequest;

  try {
    const data = await api.getVideoContent(body);
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
- **Accept**: `video/mp4`, `application/json`


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | The generated video stream. |  -  |
| **401** | Missing or invalid API key (OpenAI error envelope). |  * X-Deeprelay-Error-Code -  <br>  |
| **403** | API key lacks the required scope (&#x60;insufficient_scope&#x60;), or the key has a model allowlist that does not include the requested model (&#x60;model_not_allowed_for_key&#x60;; also the answer for a model that does not exist, so a restricted key cannot probe the catalog). OpenAI error envelope. |  * X-Deeprelay-Error-Code -  <br>  |
| **404** | Model or resource not found (OpenAI error envelope). |  * X-Deeprelay-Error-Code -  <br>  |
| **410** | The requested artifact has expired and is no longer available (OpenAI error envelope). |  * X-Deeprelay-Error-Code -  <br>  |
| **429** | Rate limit or subscription quota exceeded (OpenAI error envelope). A per-key or per-IP rate limit (&#x60;rate_limit_exceeded&#x60;) carries Retry-After, the whole seconds to wait, rounded up (minimum 1), and retry-after-ms, the exact wait; both are the time until one request is allowed, not a full refill. A per-key denial also carries the x-ratelimit-*-requests headers. A subscription quota denial (&#x60;subscription_quota_exhausted&#x60;, raised only when the wallet cannot cover the pay-as-you-go fallback) carries &#x60;x-should-retry: false&#x60; and no Retry-After. When the tripped gate is a rolling 7-day cap (&#x60;param: weekly_input_tokens&#x60; or &#x60;param: weekly_output_tokens&#x60;), the error object also carries &#x60;quota_frees_at&#x60;, the RFC 3339 time the window frees enough capacity — the earlier of the two windows. &#x60;param&#x60; names the tripped gate: monthly_input_tokens, monthly_output_tokens, weekly_input_tokens, weekly_output_tokens, max_usage, input_overshoot (this request\&#39;s estimated input alone exceeds what is left in the tighter of the monthly and rolling 7-day input allowances), or output_overshoot (the same for the estimated output — the completion bound). On an overshoot the quota is not exhausted — send a smaller request (or a smaller max_tokens) or add credits. |  * X-Deeprelay-Requested-Model -  <br>  * X-Deeprelay-Fallback-Attempted -  <br>  * Retry-After - Seconds the client should wait before retrying. <br>  * retry-after-ms -  <br>  * x-ratelimit-limit-requests -  <br>  * x-ratelimit-remaining-requests -  <br>  * x-ratelimit-reset-requests -  <br>  * x-should-retry -  <br>  * X-Deeprelay-Error-Code -  <br>  |

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


## inferencePreflight

> InferencePreflight inferencePreflight(model)

Check whether a model request would be served, and at whose expense

Answers \&quot;what happens if I call this model right now?\&quot; before the call is made: whether the plan covers the model, whether the organization is subscribed, and whether there is credit to pay if it is not covered. Requires the &#x60;serverless:read&#x60; scope.  Nothing is sent, counted, charged, or reserved. The verdict is computed from the state of the SAME gates that judge the real request — plan coverage, subscription entitlement, remaining plan quota, credit balance and self-set spending caps — so the advice cannot drift from enforcement. It is deliberately NOT a dry run: no per-request cost estimate is quoted, because that figure changes with every prompt and quoting it would invite clients to cache it.  The gates consulted depend on the model\&#39;s MODALITY, because the endpoints do not all meet the same ones. Chat, embeddings and image requests meet the full gate (balance, then the organization\&#39;s opt-in daily cap, then its monthly cap). Video creation meets only the balance check, so an organization past its own spending cap but holding credit is reported as fundable for video — which is what the video endpoint will in fact do. Predicting the strictest gate rather than the applicable one would make this endpoint refuse requests the API accepts.  The same is true of the plan: video creation does not run the subscription gate, so &#x60;plan_covered&#x60; is false for a video model even if an operator has placed it on the plan\&#39;s covered list. That is a deliberate divergence from the same-named field on &#x60;/v1/models&#x60;, which reports the platform\&#39;s configuration. Here it means \&quot;the plan covers this REQUEST\&quot; — describing what will happen is the entire job of a preflight.  One caveat on \&quot;read-only\&quot;: resolving the balance creates the organization\&#39;s balance row if it has never had one (idempotent, org-scoped, and the same row the first real request would create). Nothing else is written.  The case this exists for is &#x60;warn&#x60; / &#x60;not_plan_covered&#x60;. A subscriber calling a model outside the plan IS served and IS charged pay-as-you-go, and nothing in the response to that request says so — the first signal used to be the invoice.  &#x60;funded&#x60; is a boolean and never a figure. This route is on the inference read scope, so it must not disclose the organization\&#39;s balance; use &#x60;/billing/balance&#x60; for the number.  Failure posture is the opposite of the request gate\&#39;s: any gate that cannot be read degrades the verdict toward &#x60;ok&#x60;, never toward &#x60;block&#x60;. A false &#x60;block&#x60; would stop a customer whose request would have succeeded, while a false &#x60;ok&#x60; costs them one honest error from the real call. 

### Example

```ts
import {
  Configuration,
  InferenceApi,
} from '@deeprelay/sdk';
import type { InferencePreflightRequest } from '@deeprelay/sdk';

async function example() {
  console.log("🚀 Testing @deeprelay/sdk SDK...");
  const config = new Configuration({ 
    // Configure HTTP bearer authorization: bearerAuth
    accessToken: "YOUR BEARER TOKEN",
  });
  const api = new InferenceApi(config);

  const body = {
    // string | Model id or alias, optionally with a `:economy` tier suffix. It is resolved through the catalog exactly as the inference endpoints resolve it, so an alias and a tier view answer for the model that would actually serve.
    model: model_example,
  } satisfies InferencePreflightRequest;

  try {
    const data = await api.inferencePreflight(body);
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
| **model** | `string` | Model id or alias, optionally with a &#x60;:economy&#x60; tier suffix. It is resolved through the catalog exactly as the inference endpoints resolve it, so an alias and a tier view answer for the model that would actually serve. | [Defaults to `undefined`] |

### Return type

[**InferencePreflight**](InferencePreflight.md)

### Authorization

[bearerAuth](../README.md#bearerAuth)

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: `application/json`


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | OK |  -  |
| **404** | Model or resource not found (OpenAI error envelope). |  * X-Deeprelay-Error-Code -  <br>  |
| **429** | Rate limit or subscription quota exceeded (OpenAI error envelope). A per-key or per-IP rate limit (&#x60;rate_limit_exceeded&#x60;) carries Retry-After, the whole seconds to wait, rounded up (minimum 1), and retry-after-ms, the exact wait; both are the time until one request is allowed, not a full refill. A per-key denial also carries the x-ratelimit-*-requests headers. A subscription quota denial (&#x60;subscription_quota_exhausted&#x60;, raised only when the wallet cannot cover the pay-as-you-go fallback) carries &#x60;x-should-retry: false&#x60; and no Retry-After. When the tripped gate is a rolling 7-day cap (&#x60;param: weekly_input_tokens&#x60; or &#x60;param: weekly_output_tokens&#x60;), the error object also carries &#x60;quota_frees_at&#x60;, the RFC 3339 time the window frees enough capacity — the earlier of the two windows. &#x60;param&#x60; names the tripped gate: monthly_input_tokens, monthly_output_tokens, weekly_input_tokens, weekly_output_tokens, max_usage, input_overshoot (this request\&#39;s estimated input alone exceeds what is left in the tighter of the monthly and rolling 7-day input allowances), or output_overshoot (the same for the estimated output — the completion bound). On an overshoot the quota is not exhausted — send a smaller request (or a smaller max_tokens) or add credits. |  * X-Deeprelay-Requested-Model -  <br>  * X-Deeprelay-Fallback-Attempted -  <br>  * Retry-After - Seconds the client should wait before retrying. <br>  * retry-after-ms -  <br>  * x-ratelimit-limit-requests -  <br>  * x-ratelimit-remaining-requests -  <br>  * x-ratelimit-reset-requests -  <br>  * x-should-retry -  <br>  * X-Deeprelay-Error-Code -  <br>  |

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


## listModels

> ModelList listModels(modality, ifNoneMatch)

List available models (OpenAI-compatible)

Works with or without an API key, and returns the same body either way. Without a key the response is publicly cacheable (&#x60;Cache-Control: public, max-age&#x3D;60&#x60;), carries a strong &#x60;ETag&#x60; (send &#x60;If-None-Match&#x60; to get a 304), and is rate-limited per client IP (429 &#x60;rate_limit_exceeded&#x60; with Retry-After). With a key it is &#x60;Cache-Control: private&#x60; and counts against the key\&#39;s rate limit; an invalid key returns 401, it does not fall back to anonymous access. Error responses are &#x60;no-store&#x60;.  Each entry\&#39;s &#x60;supported_parameters&#x60; is backed by live capability probes of the model\&#39;s upstreams: it is the list to check before sending a gated parameter (&#x60;response_format&#x60;, &#x60;structured_outputs&#x60;, &#x60;logprobs&#x60;, &#x60;tools&#x60;, &#x60;vision&#x60;, ...).  One exception to \&quot;the same body\&quot;: a key with a model allowlist (&#x60;allowed_models&#x60;) sees only the models on its list.  Each entry may carry a &#x60;metrics&#x60; object (always the last key): measured time to first token, decode rate and success rate over a rolling window of deeprelay customer traffic. Below the sample minimum &#x60;insufficient_data&#x60; is true and the figure is omitted, never zero. 

### Example

```ts
import {
  Configuration,
  InferenceApi,
} from '@deeprelay/sdk';
import type { ListModelsRequest } from '@deeprelay/sdk';

async function example() {
  console.log("🚀 Testing @deeprelay/sdk SDK...");
  const config = new Configuration({ 
    // Configure HTTP bearer authorization: bearerAuth
    accessToken: "YOUR BEARER TOKEN",
  });
  const api = new InferenceApi(config);

  const body = {
    // 'chat' | 'image' | 'video' | 'embedding' (optional)
    modality: modality_example,
    // string | An ETag from an earlier anonymous response; a match returns 304. (optional)
    ifNoneMatch: ifNoneMatch_example,
  } satisfies ListModelsRequest;

  try {
    const data = await api.listModels(body);
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
| **modality** | `chat`, `image`, `video`, `embedding` |  | [Optional] [Defaults to `undefined`] [Enum: chat, image, video, embedding] |
| **ifNoneMatch** | `string` | An ETag from an earlier anonymous response; a match returns 304. | [Optional] [Defaults to `undefined`] |

### Return type

[**ModelList**](ModelList.md)

### Authorization

[bearerAuth](../README.md#bearerAuth)

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: `application/json`


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | OpenAI-shaped model list. |  * Cache-Control - &#x60;public, max-age&#x3D;60&#x60; without a key; &#x60;private&#x60; with one. <br>  * ETag - Strong validator for the anonymous listing. <br>  |
| **304** | Not modified; the If-None-Match ETag still matches. |  -  |
| **400** | Invalid request (OpenAI error envelope). |  * X-Deeprelay-Requested-Model -  <br>  * X-Deeprelay-Fallback-Attempted -  <br>  * X-Deeprelay-Error-Code -  <br>  |
| **401** | Missing or invalid API key (OpenAI error envelope). |  * X-Deeprelay-Error-Code -  <br>  |
| **403** | API key lacks the required scope (&#x60;insufficient_scope&#x60;), or the key has a model allowlist that does not include the requested model (&#x60;model_not_allowed_for_key&#x60;; also the answer for a model that does not exist, so a restricted key cannot probe the catalog). OpenAI error envelope. |  * X-Deeprelay-Error-Code -  <br>  |
| **429** | Rate limit or subscription quota exceeded (OpenAI error envelope). A per-key or per-IP rate limit (&#x60;rate_limit_exceeded&#x60;) carries Retry-After, the whole seconds to wait, rounded up (minimum 1), and retry-after-ms, the exact wait; both are the time until one request is allowed, not a full refill. A per-key denial also carries the x-ratelimit-*-requests headers. A subscription quota denial (&#x60;subscription_quota_exhausted&#x60;, raised only when the wallet cannot cover the pay-as-you-go fallback) carries &#x60;x-should-retry: false&#x60; and no Retry-After. When the tripped gate is a rolling 7-day cap (&#x60;param: weekly_input_tokens&#x60; or &#x60;param: weekly_output_tokens&#x60;), the error object also carries &#x60;quota_frees_at&#x60;, the RFC 3339 time the window frees enough capacity — the earlier of the two windows. &#x60;param&#x60; names the tripped gate: monthly_input_tokens, monthly_output_tokens, weekly_input_tokens, weekly_output_tokens, max_usage, input_overshoot (this request\&#39;s estimated input alone exceeds what is left in the tighter of the monthly and rolling 7-day input allowances), or output_overshoot (the same for the estimated output — the completion bound). On an overshoot the quota is not exhausted — send a smaller request (or a smaller max_tokens) or add credits. |  * X-Deeprelay-Requested-Model -  <br>  * X-Deeprelay-Fallback-Attempted -  <br>  * Retry-After - Seconds the client should wait before retrying. <br>  * retry-after-ms -  <br>  * x-ratelimit-limit-requests -  <br>  * x-ratelimit-remaining-requests -  <br>  * x-ratelimit-reset-requests -  <br>  * x-should-retry -  <br>  * X-Deeprelay-Error-Code -  <br>  |

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


## listVideos

> VideoList listVideos(after, limit)

List video generation jobs

### Example

```ts
import {
  Configuration,
  InferenceApi,
} from '@deeprelay/sdk';
import type { ListVideosRequest } from '@deeprelay/sdk';

async function example() {
  console.log("🚀 Testing @deeprelay/sdk SDK...");
  const config = new Configuration({ 
    // Configure HTTP bearer authorization: bearerAuth
    accessToken: "YOUR BEARER TOKEN",
  });
  const api = new InferenceApi(config);

  const body = {
    // string (optional)
    after: after_example,
    // number (optional)
    limit: 56,
  } satisfies ListVideosRequest;

  try {
    const data = await api.listVideos(body);
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
| **limit** | `number` |  | [Optional] [Defaults to `undefined`] |

### Return type

[**VideoList**](VideoList.md)

### Authorization

[bearerAuth](../README.md#bearerAuth)

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: `application/json`


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | A page of video generation jobs. |  -  |
| **401** | Missing or invalid API key (OpenAI error envelope). |  * X-Deeprelay-Error-Code -  <br>  |
| **403** | API key lacks the required scope (&#x60;insufficient_scope&#x60;), or the key has a model allowlist that does not include the requested model (&#x60;model_not_allowed_for_key&#x60;; also the answer for a model that does not exist, so a restricted key cannot probe the catalog). OpenAI error envelope. |  * X-Deeprelay-Error-Code -  <br>  |
| **429** | Rate limit or subscription quota exceeded (OpenAI error envelope). A per-key or per-IP rate limit (&#x60;rate_limit_exceeded&#x60;) carries Retry-After, the whole seconds to wait, rounded up (minimum 1), and retry-after-ms, the exact wait; both are the time until one request is allowed, not a full refill. A per-key denial also carries the x-ratelimit-*-requests headers. A subscription quota denial (&#x60;subscription_quota_exhausted&#x60;, raised only when the wallet cannot cover the pay-as-you-go fallback) carries &#x60;x-should-retry: false&#x60; and no Retry-After. When the tripped gate is a rolling 7-day cap (&#x60;param: weekly_input_tokens&#x60; or &#x60;param: weekly_output_tokens&#x60;), the error object also carries &#x60;quota_frees_at&#x60;, the RFC 3339 time the window frees enough capacity — the earlier of the two windows. &#x60;param&#x60; names the tripped gate: monthly_input_tokens, monthly_output_tokens, weekly_input_tokens, weekly_output_tokens, max_usage, input_overshoot (this request\&#39;s estimated input alone exceeds what is left in the tighter of the monthly and rolling 7-day input allowances), or output_overshoot (the same for the estimated output — the completion bound). On an overshoot the quota is not exhausted — send a smaller request (or a smaller max_tokens) or add credits. |  * X-Deeprelay-Requested-Model -  <br>  * X-Deeprelay-Fallback-Attempted -  <br>  * Retry-After - Seconds the client should wait before retrying. <br>  * retry-after-ms -  <br>  * x-ratelimit-limit-requests -  <br>  * x-ratelimit-remaining-requests -  <br>  * x-ratelimit-reset-requests -  <br>  * x-should-retry -  <br>  * X-Deeprelay-Error-Code -  <br>  |

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)

