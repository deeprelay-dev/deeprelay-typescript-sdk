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
| **401** | Missing or invalid API key (OpenAI error envelope). |  -  |
| **403** | API key lacks the required scope (OpenAI error envelope). |  -  |
| **404** | Model or resource not found (OpenAI error envelope). |  -  |
| **409** | Invalid request (OpenAI error envelope). |  -  |
| **429** | Rate limit exceeded (OpenAI error envelope). Retry-After header indicates seconds to wait. |  * Retry-After - Seconds the client should wait before retrying. <br>  |

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


## createChatCompletion

> ChatCompletionResponse createChatCompletion(chatCompletionRequest)

Create a chat completion (OpenAI-compatible)

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
| **200** | Successful response. application/json for non-streaming requests; text/event-stream for streaming requests (stream&#x3D;true).  |  -  |
| **400** | Invalid request (OpenAI error envelope). |  -  |
| **401** | Missing or invalid API key (OpenAI error envelope). |  -  |
| **402** | Insufficient balance (OpenAI error envelope, SERV-06). |  -  |
| **403** | API key lacks the required scope (OpenAI error envelope). |  -  |
| **404** | Model or resource not found (OpenAI error envelope). |  -  |
| **422** | Request validation failed (OpenAI error envelope). |  -  |
| **429** | Rate limit exceeded (OpenAI error envelope). Retry-After header indicates seconds to wait. |  * Retry-After - Seconds the client should wait before retrying. <br>  |
| **500** | Internal server error (OpenAI error envelope). |  -  |
| **503** | Upstream provider unavailable (OpenAI error envelope). Retry-After header may indicate seconds to wait. |  * Retry-After - Seconds the client should wait before retrying. <br>  |

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


## createEmbeddings

> EmbeddingsResponse createEmbeddings(embeddingsRequest)

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
| **400** | Invalid request (OpenAI error envelope). |  -  |
| **401** | Missing or invalid API key (OpenAI error envelope). |  -  |
| **402** | Insufficient balance (OpenAI error envelope, SERV-06). |  -  |
| **403** | API key lacks the required scope (OpenAI error envelope). |  -  |
| **404** | Model or resource not found (OpenAI error envelope). |  -  |
| **413** | Request body too large (OpenAI error envelope, code request_too_large). |  -  |
| **429** | Rate limit exceeded (OpenAI error envelope). Retry-After header indicates seconds to wait. |  * Retry-After - Seconds the client should wait before retrying. <br>  |
| **500** | Internal server error (OpenAI error envelope). |  -  |
| **502** | The upstream answered but its response could not be used (OpenAI error envelope): code upstream_response_too_large when the vector payload exceeded the per-request size limit, or upstream_error for a malformed / misaligned response. Not retryable as-is for upstream_response_too_large — send fewer inputs. |  -  |
| **503** | Upstream provider unavailable (OpenAI error envelope). Retry-After header may indicate seconds to wait. |  * Retry-After - Seconds the client should wait before retrying. <br>  |
| **504** | Upstream provider exceeded the synchronous per-attempt deadline (OpenAI error envelope). 504 semantic — distinct from 503 OpenAIUpstreamUnavailable which signals a connection or routing failure rather than a timeout.  |  -  |

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


## createImage

> ImagesResponse createImage(imagesGenerationsRequest, idempotencyKey)

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
| **400** | Invalid request (OpenAI error envelope). |  -  |
| **401** | Missing or invalid API key (OpenAI error envelope). |  -  |
| **402** | Insufficient balance (OpenAI error envelope, SERV-06). |  -  |
| **403** | API key lacks the required scope (OpenAI error envelope). |  -  |
| **404** | Model or resource not found (OpenAI error envelope). |  -  |
| **422** | Request validation failed (OpenAI error envelope). |  -  |
| **429** | Rate limit exceeded (OpenAI error envelope). Retry-After header indicates seconds to wait. |  * Retry-After - Seconds the client should wait before retrying. <br>  |
| **500** | Internal server error (OpenAI error envelope). |  -  |
| **503** | Upstream provider unavailable (OpenAI error envelope). Retry-After header may indicate seconds to wait. |  * Retry-After - Seconds the client should wait before retrying. <br>  |
| **504** | Upstream provider exceeded the synchronous per-attempt deadline (OpenAI error envelope). 504 semantic — distinct from 503 OpenAIUpstreamUnavailable which signals a connection or routing failure rather than a timeout.  |  -  |

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


## createVideo

> VideoJob createVideo(videoCreateRequest, idempotencyKey)

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
| **400** | Invalid request (OpenAI error envelope). |  -  |
| **401** | Missing or invalid API key (OpenAI error envelope). |  -  |
| **402** | Insufficient balance (OpenAI error envelope, SERV-06). |  -  |
| **403** | API key lacks the required scope (OpenAI error envelope). |  -  |
| **404** | Model or resource not found (OpenAI error envelope). |  -  |
| **429** | Rate limit exceeded (OpenAI error envelope). Retry-After header indicates seconds to wait. |  * Retry-After - Seconds the client should wait before retrying. <br>  |
| **500** | Internal server error (OpenAI error envelope). |  -  |

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


## getModel

> Model getModel(id)

Get a specific model (OpenAI-compatible)

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
| **401** | Missing or invalid API key (OpenAI error envelope). |  -  |
| **403** | API key lacks the required scope (OpenAI error envelope). |  -  |
| **404** | Model or resource not found (OpenAI error envelope). |  -  |
| **429** | Rate limit exceeded (OpenAI error envelope). Retry-After header indicates seconds to wait. |  * Retry-After - Seconds the client should wait before retrying. <br>  |

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
| **401** | Missing or invalid API key (OpenAI error envelope). |  -  |
| **403** | API key lacks the required scope (OpenAI error envelope). |  -  |
| **404** | Model or resource not found (OpenAI error envelope). |  -  |
| **429** | Rate limit exceeded (OpenAI error envelope). Retry-After header indicates seconds to wait. |  * Retry-After - Seconds the client should wait before retrying. <br>  |

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
| **401** | Missing or invalid API key (OpenAI error envelope). |  -  |
| **403** | API key lacks the required scope (OpenAI error envelope). |  -  |
| **404** | Model or resource not found (OpenAI error envelope). |  -  |
| **410** | The requested artifact has expired and is no longer available (OpenAI error envelope). |  -  |
| **429** | Rate limit exceeded (OpenAI error envelope). Retry-After header indicates seconds to wait. |  * Retry-After - Seconds the client should wait before retrying. <br>  |

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
| **404** | Model or resource not found (OpenAI error envelope). |  -  |
| **429** | Rate limit exceeded (OpenAI error envelope). Retry-After header indicates seconds to wait. |  * Retry-After - Seconds the client should wait before retrying. <br>  |

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


## listModels

> ModelList listModels(modality)

List available models (OpenAI-compatible)

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
| **200** | OpenAI-shaped model list. |  -  |
| **400** | Invalid request (OpenAI error envelope). |  -  |
| **401** | Missing or invalid API key (OpenAI error envelope). |  -  |
| **403** | API key lacks the required scope (OpenAI error envelope). |  -  |
| **429** | Rate limit exceeded (OpenAI error envelope). Retry-After header indicates seconds to wait. |  * Retry-After - Seconds the client should wait before retrying. <br>  |

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
| **401** | Missing or invalid API key (OpenAI error envelope). |  -  |
| **403** | API key lacks the required scope (OpenAI error envelope). |  -  |
| **429** | Rate limit exceeded (OpenAI error envelope). Retry-After header indicates seconds to wait. |  * Retry-After - Seconds the client should wait before retrying. <br>  |

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)

