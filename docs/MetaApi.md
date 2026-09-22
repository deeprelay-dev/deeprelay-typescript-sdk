# MetaApi

All URIs are relative to *https://api.deeprelay.ai/v1*

| Method | HTTP request | Description |
|------------- | ------------- | -------------|
| [**getHealth**](MetaApi.md#gethealth) | **GET** /health | Liveness probe |
| [**getOpenApiSpec**](MetaApi.md#getopenapispec) | **GET** /openapi.json | OpenAPI 3.1 specification |



## getHealth

> GetHealth200Response getHealth()

Liveness probe

### Example

```ts
import {
  Configuration,
  MetaApi,
} from '@deeprelay/sdk';
import type { GetHealthRequest } from '@deeprelay/sdk';

async function example() {
  console.log("🚀 Testing @deeprelay/sdk SDK...");
  const api = new MetaApi();

  try {
    const data = await api.getHealth();
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

[**GetHealth200Response**](GetHealth200Response.md)

### Authorization

No authorization required

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: `application/json`


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | OK |  -  |

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


## getOpenApiSpec

> object getOpenApiSpec()

OpenAPI 3.1 specification

The machine-readable specification of the PUBLISHED API surface — the same document the client SDKs are generated from. Endpoints marked &#x60;x-gpu-supply-paused&#x60; in the authoritative spec are absent from it while GPU supply is paused (D-28), so this response and the SDKs always describe the same surface.

### Example

```ts
import {
  Configuration,
  MetaApi,
} from '@deeprelay/sdk';
import type { GetOpenApiSpecRequest } from '@deeprelay/sdk';

async function example() {
  console.log("🚀 Testing @deeprelay/sdk SDK...");
  const api = new MetaApi();

  try {
    const data = await api.getOpenApiSpec();
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

**object**

### Authorization

No authorization required

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: `application/json`


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | OK |  -  |

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)

