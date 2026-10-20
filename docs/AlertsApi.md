# AlertsApi

All URIs are relative to *https://api.deeprelay.ai/v1*

| Method | HTTP request | Description |
|------------- | ------------- | -------------|
| [**getAlertSettings**](AlertsApi.md#getalertsettings) | **GET** /alerts/settings | Get the organization\&#39;s alert settings |
| [**putAlertSettings**](AlertsApi.md#putalertsettings) | **PUT** /alerts/settings | Replace the organization\&#39;s alert settings |



## getAlertSettings

> AlertSettings getAlertSettings()

Get the organization\&#39;s alert settings

Returns the low-balance threshold and the four org-level alert email toggles. An organization that has never saved settings gets the defaults with &#x60;updated_at: null&#x60;. Requires the &#x60;billing:read&#x60; scope. 

### Example

```ts
import {
  Configuration,
  AlertsApi,
} from '@deeprelay/sdk';
import type { GetAlertSettingsRequest } from '@deeprelay/sdk';

async function example() {
  console.log("🚀 Testing @deeprelay/sdk SDK...");
  const config = new Configuration({ 
    // Configure HTTP bearer authorization: bearerAuth
    accessToken: "YOUR BEARER TOKEN",
  });
  const api = new AlertsApi(config);

  try {
    const data = await api.getAlertSettings();
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

[**AlertSettings**](AlertSettings.md)

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


## putAlertSettings

> AlertSettings putAlertSettings(alertSettingsUpdate)

Replace the organization\&#39;s alert settings

Replaces every setting at once: send &#x60;balance_threshold_cents&#x60; and all four &#x60;email&#x60; toggles (a missing field is 422 &#x60;validation_failed&#x60; naming the &#x60;field&#x60;). Requires the &#x60;billing:write&#x60; scope AND an org admin\&#39;s key or a &#x60;full_access&#x60; key (403 &#x60;forbidden&#x60; otherwise). The toggles only control the org-level emails; a member always receives their own spend-limit emails. Webhook delivery of the same events is configured on the webhook endpoint, not here. 

### Example

```ts
import {
  Configuration,
  AlertsApi,
} from '@deeprelay/sdk';
import type { PutAlertSettingsRequest } from '@deeprelay/sdk';

async function example() {
  console.log("🚀 Testing @deeprelay/sdk SDK...");
  const config = new Configuration({ 
    // Configure HTTP bearer authorization: bearerAuth
    accessToken: "YOUR BEARER TOKEN",
  });
  const api = new AlertsApi(config);

  const body = {
    // AlertSettingsUpdate
    alertSettingsUpdate: ...,
  } satisfies PutAlertSettingsRequest;

  try {
    const data = await api.putAlertSettings(body);
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
| **alertSettingsUpdate** | [AlertSettingsUpdate](AlertSettingsUpdate.md) |  | |

### Return type

[**AlertSettings**](AlertSettings.md)

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
| **422** | Error response (RFC 7807) |  -  |
| **429** | Rate limit exceeded (RFC 7807). Retry-After header indicates seconds to wait. |  * Retry-After - Seconds the client should wait before retrying. <br>  |
| **0** | Error response (RFC 7807) |  -  |

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)

