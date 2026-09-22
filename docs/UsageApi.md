# UsageApi

All URIs are relative to *https://api.deeprelay.ai/v1*

| Method | HTTP request | Description |
|------------- | ------------- | -------------|
| [**listUsage**](UsageApi.md#listusage) | **GET** /usage | Time-bucketed usage |



## listUsage

> UsagePage listUsage(bucket, groupBy, start, end, cursor, limit)

Time-bucketed usage

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
    // 'hour' | 'day' | 'week' | 'month' (optional)
    bucket: bucket_example,
    // 'instance_id' | 'gpu_type' (optional)
    groupBy: groupBy_example,
    // Date (optional)
    start: 2013-10-20T19:20:30+01:00,
    // Date (optional)
    end: 2013-10-20T19:20:30+01:00,
    // string (optional)
    cursor: cursor_example,
    // number (optional)
    limit: 56,
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
| **bucket** | `hour`, `day`, `week`, `month` |  | [Optional] [Defaults to `undefined`] [Enum: hour, day, week, month] |
| **groupBy** | `instance_id`, `gpu_type` |  | [Optional] [Defaults to `undefined`] [Enum: instance_id, gpu_type] |
| **start** | `Date` |  | [Optional] [Defaults to `undefined`] |
| **end** | `Date` |  | [Optional] [Defaults to `undefined`] |
| **cursor** | `string` |  | [Optional] [Defaults to `undefined`] |
| **limit** | `number` |  | [Optional] [Defaults to `50`] |

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

