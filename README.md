# @deeprelay/sdk@0.2.1

A TypeScript SDK client for the api.deeprelay.ai API.

## Usage

First, install the SDK from npm.

```bash
npm install @deeprelay/sdk --save
```

Next, try it out.


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


## Documentation

### API Endpoints

All URIs are relative to *https://api.deeprelay.ai/v1*

| Class | Method | HTTP request | Description
| ----- | ------ | ------------ | -------------
*BillingApi* | [**createCryptoDeposit**](docs/BillingApi.md#createcryptodepositoperation) | **POST** /billing/deposits/crypto | Create a stablecoin deposit
*BillingApi* | [**createSubscriptionCheckout**](docs/BillingApi.md#createsubscriptioncheckout) | **POST** /billing/subscription/checkout | Start a subscription checkout session
*BillingApi* | [**createSubscriptionPortal**](docs/BillingApi.md#createsubscriptionportal) | **POST** /billing/subscription/portal | Open the billing portal to cancel or manage the subscription
*BillingApi* | [**deleteSpendingLimit**](docs/BillingApi.md#deletespendinglimit) | **DELETE** /billing/spending-limit | Clear the org spending limit
*BillingApi* | [**getBalance**](docs/BillingApi.md#getbalance) | **GET** /billing/balance | Get the org credit balance
*BillingApi* | [**getDeposit**](docs/BillingApi.md#getdeposit) | **GET** /billing/deposits/{id} | Get one stablecoin deposit
*BillingApi* | [**getReferral**](docs/BillingApi.md#getreferral) | **GET** /referrals | Get the org referral code, invite link, terms and stats
*BillingApi* | [**getSpendingLimit**](docs/BillingApi.md#getspendinglimit) | **GET** /billing/spending-limit | Get the org spending limit
*BillingApi* | [**getSubscription**](docs/BillingApi.md#getsubscription) | **GET** /billing/subscription | Get the org subscription status and quota usage
*BillingApi* | [**listDeposits**](docs/BillingApi.md#listdeposits) | **GET** /billing/deposits | List stablecoin deposits
*BillingApi* | [**updateSpendingLimit**](docs/BillingApi.md#updatespendinglimitoperation) | **PUT** /billing/spending-limit | Set the org spending limit
*InferenceApi* | [**cancelVideo**](docs/InferenceApi.md#cancelvideo) | **POST** /videos/{id}/cancel | Cancel a video generation job
*InferenceApi* | [**createChatCompletion**](docs/InferenceApi.md#createchatcompletion) | **POST** /chat/completions | Create a chat completion (OpenAI-compatible)
*InferenceApi* | [**createEmbeddings**](docs/InferenceApi.md#createembeddings) | **POST** /embeddings | Create embeddings (OpenAI-compatible)
*InferenceApi* | [**createImage**](docs/InferenceApi.md#createimage) | **POST** /images/generations | Create image (OpenAI-compatible)
*InferenceApi* | [**createVideo**](docs/InferenceApi.md#createvideo) | **POST** /videos | Create a video generation job (async)
*InferenceApi* | [**getModel**](docs/InferenceApi.md#getmodel) | **GET** /models/{id} | Get a specific model (OpenAI-compatible)
*InferenceApi* | [**getVideo**](docs/InferenceApi.md#getvideo) | **GET** /videos/{id} | Get a video generation job
*InferenceApi* | [**getVideoContent**](docs/InferenceApi.md#getvideocontent) | **GET** /videos/{id}/content | Download a completed video artifact
*InferenceApi* | [**inferencePreflight**](docs/InferenceApi.md#inferencepreflight) | **GET** /inference/preflight | Check whether a model request would be served, and at whose expense
*InferenceApi* | [**listModels**](docs/InferenceApi.md#listmodels) | **GET** /models | List available models (OpenAI-compatible)
*InferenceApi* | [**listVideos**](docs/InferenceApi.md#listvideos) | **GET** /videos | List video generation jobs
*MetaApi* | [**getHealth**](docs/MetaApi.md#gethealth) | **GET** /health | Liveness probe
*MetaApi* | [**getOpenApiSpec**](docs/MetaApi.md#getopenapispec) | **GET** /openapi.json | OpenAPI 3.1 specification
*UsageApi* | [**listUsage**](docs/UsageApi.md#listusage) | **GET** /usage | Time-bucketed usage
*WebhooksApi* | [**createWebhookEndpoint**](docs/WebhooksApi.md#createwebhookendpointoperation) | **POST** /webhook-endpoints | Create a webhook endpoint
*WebhooksApi* | [**deleteWebhookEndpoint**](docs/WebhooksApi.md#deletewebhookendpoint) | **DELETE** /webhook-endpoints/{id} | Delete a webhook endpoint
*WebhooksApi* | [**getWebhookEndpoint**](docs/WebhooksApi.md#getwebhookendpoint) | **GET** /webhook-endpoints/{id} | Get a webhook endpoint
*WebhooksApi* | [**listWebhookEndpoints**](docs/WebhooksApi.md#listwebhookendpoints) | **GET** /webhook-endpoints | List webhook endpoints


### Models

- [Balance](docs/Balance.md)
- [ChatChoice](docs/ChatChoice.md)
- [ChatCompletionRequest](docs/ChatCompletionRequest.md)
- [ChatCompletionResponse](docs/ChatCompletionResponse.md)
- [ChatMessage](docs/ChatMessage.md)
- [CreateCryptoDepositRequest](docs/CreateCryptoDepositRequest.md)
- [CreateWebhookEndpointRequest](docs/CreateWebhookEndpointRequest.md)
- [CryptoDeposit](docs/CryptoDeposit.md)
- [Embedding](docs/Embedding.md)
- [EmbeddingsRequest](docs/EmbeddingsRequest.md)
- [EmbeddingsRequestInput](docs/EmbeddingsRequestInput.md)
- [EmbeddingsResponse](docs/EmbeddingsResponse.md)
- [EmbeddingsUsage](docs/EmbeddingsUsage.md)
- [GetHealth200Response](docs/GetHealth200Response.md)
- [ImagesGenerationsRequest](docs/ImagesGenerationsRequest.md)
- [ImagesResponse](docs/ImagesResponse.md)
- [ImagesResponseDataInner](docs/ImagesResponseDataInner.md)
- [ImagesResponseUsage](docs/ImagesResponseUsage.md)
- [InferencePreflight](docs/InferencePreflight.md)
- [ListDeposits200Response](docs/ListDeposits200Response.md)
- [Model](docs/Model.md)
- [ModelList](docs/ModelList.md)
- [ModelParametersInner](docs/ModelParametersInner.md)
- [ModelPricing](docs/ModelPricing.md)
- [ModelRate](docs/ModelRate.md)
- [OpenAIErrorEnvelope](docs/OpenAIErrorEnvelope.md)
- [OpenAIErrorEnvelopeError](docs/OpenAIErrorEnvelopeError.md)
- [PeakWindow](docs/PeakWindow.md)
- [Problem](docs/Problem.md)
- [RefereeStatus](docs/RefereeStatus.md)
- [Referral](docs/Referral.md)
- [SpendingLimit](docs/SpendingLimit.md)
- [StreamOptions](docs/StreamOptions.md)
- [Subscription](docs/Subscription.md)
- [SubscriptionCheckoutRequest](docs/SubscriptionCheckoutRequest.md)
- [SubscriptionCheckoutSession](docs/SubscriptionCheckoutSession.md)
- [SubscriptionPlan](docs/SubscriptionPlan.md)
- [SubscriptionPortalRequest](docs/SubscriptionPortalRequest.md)
- [SubscriptionPortalSession](docs/SubscriptionPortalSession.md)
- [SubscriptionPrice](docs/SubscriptionPrice.md)
- [SubscriptionQuota](docs/SubscriptionQuota.md)
- [SubscriptionUsage](docs/SubscriptionUsage.md)
- [UpdateSpendingLimitRequest](docs/UpdateSpendingLimitRequest.md)
- [Usage](docs/Usage.md)
- [UsageBucket](docs/UsageBucket.md)
- [UsagePage](docs/UsagePage.md)
- [VideoCreateRequest](docs/VideoCreateRequest.md)
- [VideoJob](docs/VideoJob.md)
- [VideoList](docs/VideoList.md)
- [WebhookEndpoint](docs/WebhookEndpoint.md)
- [WebhookEndpointPage](docs/WebhookEndpointPage.md)

### Authorization


Authentication schemes defined for the API:
<a id="bearerAuth"></a>
#### bearerAuth


- **Type**: HTTP Bearer Token authentication (deeprelay_live_<24-base62>)

## About

This TypeScript SDK client supports the [Fetch API](https://fetch.spec.whatwg.org/)
and is automatically generated by the
[OpenAPI Generator](https://openapi-generator.tech) project:

- API version: `1.0.0`
- Package version: `0.2.1`
- Generator version: `7.24.0`
- Build package: `org.openapitools.codegen.languages.TypeScriptFetchClientCodegen`

The generated npm module supports the following:

- Environments
  * Node.js
  * Webpack
  * Browserify
- Language levels
  * ES5 - you must have a Promises/A+ library installed
  * ES6
- Module systems
  * CommonJS
  * ES6 module system


## Development

### Building

To build the TypeScript source code, you need to have Node.js and npm installed.
After cloning the repository, navigate to the project directory and run:

```bash
npm install
npm run build
```

### Publishing

Once you've built the package, you can publish it to npm:

```bash
npm publish
```

## License

[Apache-2.0]()
