# UsageApi

All URIs are relative to *https://api.deeprelay.ai/v1*

| Method | HTTP request | Description |
|------------- | ------------- | -------------|
| [**listUsage**](UsageApi.md#listusage) | **GET** /usage | Time-bucketed usage |



## listUsage

> UsagePage listUsage(bucket, groupBy, start, end, cursor, limit, modality, model)

Time-bucketed usage

Returns spend aggregated into time buckets over &#x60;[start, end)&#x60; (default: the last 30 days, &#x60;bucket&#x3D;day&#x60;), newest bucket first.  The response has one of two row shapes, selected by the query:  - **Inference usage** — set &#x60;modality&#x60; and/or &#x60;model&#x60;. Rows aggregate serverless inference calls, one row per (bucket, modality, model), and carry &#x60;modality&#x60;, &#x60;model&#x60;, &#x60;prompt_tokens&#x60;, &#x60;completion_tokens&#x60; and &#x60;image_count&#x60;. This is the usage a serverless-inference customer is billed for. - **Instance usage** — neither &#x60;modality&#x60; nor &#x60;model&#x60; set. Rows aggregate GPU instance billing sessions, optionally split by &#x60;group_by&#x60;. With no instance usage this returns an empty &#x60;data&#x60; array, so to read inference spend always pass &#x60;modality&#x60; or &#x60;model&#x60;.  Requires the &#x60;billing:read&#x60; scope. 

### Example

```ts
import {
  Configuration,
  UsageApi,
} from '@deeprelay/sdk';
import type { ListUsageRequest } from '@deeprelay/sdk';

async function example() {
  console.log("🚀 Testing @deeprelay/sdk SDK...");
  const config = new Configuration({ 
    // Configure HTTP bearer authorization: bearerAuth
    accessToken: "YOUR BEARER TOKEN",
  });
  const api = new UsageApi(config);

  const body = {
    // 'hour' | 'day' | 'week' | 'month' | Bucket width. Defaults to `day`. (optional)
    bucket: bucket_example,
    // 'instance_id' | 'gpu_type' | Split instance-usage rows by instance or GPU type. Applies only to the instance-usage shape (neither `modality` nor `model` set); ignored when either is set, since inference rows are always split by modality and model.  (optional)
    groupBy: groupBy_example,
    // Date | Inclusive RFC 3339 range start. Defaults to 30 days ago. (optional)
    start: 2013-10-20T19:20:30+01:00,
    // Date | Exclusive RFC 3339 range end. Defaults to now; must be after `start`. (optional)
    end: 2013-10-20T19:20:30+01:00,
    // string (optional)
    cursor: cursor_example,
    // number (optional)
    limit: 56,
    // 'chat' | 'image' | 'video' | 'embedding' | Return inference-usage rows for this modality only. Setting `modality` or `model` selects the inference-usage shape; omit both for the instance-usage shape.  (optional)
    modality: modality_example,
    // string | Return inference-usage rows for this model only: an exact match on the model `id` as listed by `GET /models`. May be combined with `modality`. Setting `modality` or `model` selects the inference-usage shape.  (optional)
    model: model_example,
  } satisfies ListUsageRequest;

  try {
    const data = await api.listUsage(body);
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
| **bucket** | `hour`, `day`, `week`, `month` | Bucket width. Defaults to &#x60;day&#x60;. | [Optional] [Defaults to `undefined`] [Enum: hour, day, week, month] |
| **groupBy** | `instance_id`, `gpu_type` | Split instance-usage rows by instance or GPU type. Applies only to the instance-usage shape (neither &#x60;modality&#x60; nor &#x60;model&#x60; set); ignored when either is set, since inference rows are always split by modality and model.  | [Optional] [Defaults to `undefined`] [Enum: instance_id, gpu_type] |
| **start** | `Date` | Inclusive RFC 3339 range start. Defaults to 30 days ago. | [Optional] [Defaults to `undefined`] |
| **end** | `Date` | Exclusive RFC 3339 range end. Defaults to now; must be after &#x60;start&#x60;. | [Optional] [Defaults to `undefined`] |
| **cursor** | `string` |  | [Optional] [Defaults to `undefined`] |
| **limit** | `number` |  | [Optional] [Defaults to `50`] |
| **modality** | `chat`, `image`, `video`, `embedding` | Return inference-usage rows for this modality only. Setting &#x60;modality&#x60; or &#x60;model&#x60; selects the inference-usage shape; omit both for the instance-usage shape.  | [Optional] [Defaults to `undefined`] [Enum: chat, image, video, embedding] |
| **model** | `string` | Return inference-usage rows for this model only: an exact match on the model &#x60;id&#x60; as listed by &#x60;GET /models&#x60;. May be combined with &#x60;modality&#x60;. Setting &#x60;modality&#x60; or &#x60;model&#x60; selects the inference-usage shape.  | [Optional] [Defaults to `undefined`] |

### Return type

[**UsagePage**](UsagePage.md)

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

