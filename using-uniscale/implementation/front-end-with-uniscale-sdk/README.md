---
description: >-
  On this page, you will learn how to use the SDK with your front-end
  application.
---

# Quick start: Front-end with Uniscale SDK

This tutorial uses Uniscale's Message Threads demo solution as its base. For more detailed information on the SDK, see [library-implementation-basics](../library-implementation-basics/ "mention")



## Installation

You can find the correct SDK information in your solution or service's SDK Portal in Uniscale.

Configure registry

```
@uniscale-sdk:registry=https://sdk.uniscale.com/api/packages/8c68f0da-8a3c-45bb-abba-2b6d36aa6b3c/npm/
//sdk.uniscale.com/api/packages/8c68f0da-8a3c-45bb-abba-2b6d36aa6b3c/npm/:_authToken=eb8a29eb2b95553972f408b1feb7dedeec016106
```

Install SDK

```
npm i @uniscale-sdk/ActorCharacter-Messagethreads@1.0.6
```



## Tutorial: Using the SDK with your front-end application

Following this tutorial will help you set up a dispatcher for handling requests that communicate with the endpoints provided in the specification. A similar approach is used in this demo project: [https://github.com/uniscale/demo-ts-frontend](https://github.com/uniscale/demo-ts-frontend)



### Step 1: Implement the dispatcher&#x20;

This function will return a dispatcher which can then be used to handle any communication with the endpoints. Depending on the structure of your front-end application, you can also implement the same functionality into a dispatcher class.

#### `asSolution`

You can acquire a DispatcherSession by calling the session with `asSolution` using your solution identifier. When you have the dispatcher session, you are ready to call your endpoints. You can find your solution identifier in your solution's SDK Portal in Uniscale.

#### `withLocale`

If your service has different translations for i.e. error codes, you can define the locale you wish to use.

#### `withDataTenant`

If you have a multitenant environment, you can specify the required identifier here.

<pre class="language-typescript"><code class="lang-typescript">import { DispatcherSession, Platform } from "@uniscale-sdk/ActorCharacter-Messagethreads"

<strong>const initializeDispatcher = async (): Promise&#x3C;DispatcherSession> => {
</strong>    const session = await Platform.builder()
      .build()
    
    return session
      .asSolution("fb344616-794e-4bd7-b81a-fb1e3361701f")
      .withLocale("en-GB")
      .withDataTenant("Customer 1 data tenant")
}
</code></pre>



### Step 2: Add interceptors

These are interceptors that will call the service. The sample uses pattern interceptors to intercept all features defined below that pattern in the model. This makes it easier if you have multiple services using the same solution SDK.

To use the endpoints, we make a `POST` call on the correct URL and pass it a serialized `GatewayRequest` as defined in the SDK. The response also needs to be serialized into the `Result` class.

```typescript
import { DispatcherSession, GatewayRequest, Platform, Result } from "@uniscale-sdk/ActorCharacter-Messagethreads"
import { Patterns as AccountPatterns } from '@uniscale-sdk/ActorCharacter-Messagethreads/sdk/UniscaleDemo/Account'
import { Patterns as StreamsPatterns } from '@uniscale-sdk/ActorCharacter-Messagethreads/sdk/UniscaleDemo/Messages'

const initializeDispatcher = async (): Promise<DispatcherSession> => {
    const session = await Platform.builder()
      .withInterceptors(i => {
        i.interceptPattern(AccountPatterns.pattern, async (input, ctx) => {
            const headers = { 'Content-Type': 'application/json' }
            const response = await axios.post(
              `${URL}/api/service-to-module/` + ctx.featureId,
              GatewayRequest.from(input, ctx).toJson(),
              { headers }
            )
            return Result.fromJson(response.data)
          }
        )
        i.interceptPattern(StreamsPatterns.pattern, async (input, ctx) => {
            const headers = { 'Content-Type': 'application/json' }
            const response = await axios.post(
               `${URL}/api/service-to-module/` + ctx.featureId,
              GatewayRequest.from(input, ctx).toJson(),
              { headers }
            )
            return Result.fromJson(response.data)
          }
        )
      })
      .build()

    return session
      .asSolution("fb344616-794e-4bd7-b81a-fb1e3361701f")
      .withLocale("en-GB")
      .withDataTenant("Customer 1 data tenant")
}
```



### Step 3: Using the dispatcher&#x20;

At the base of your application, call your initialize function to get the dispatcher:

```typescript
const dispatcher = await initializeDispatcher()
```

After this, you can use endpoints to fetch your data:

```typescript
const messages = await dispatcher.request(GetDirectMessageList.with(userIdentifier))
```



## Tutorial: Using sample data from the SDK

If you want to use the endpoints provided by the SDK but don't yet have a working backend, you can register message interceptors in your dispatcher to return sample data instead of calling the real service.



### Step 1: Add mock interceptors to the dispatcher

You can either add your own mock data here or use sample data provided by the SDK.

```typescript
import { DispatcherSession, Platform } from "@uniscale-sdk/ActorCharacter-Messagethreads"
import { Patterns } from "@uniscale-sdk/ActorCharacter-Messagethreads/sdk/UniscaleDemo/Messages"
import { DirectMessageFull } from "@uniscale-sdk/ActorCharacter-Messagethreads/sdk/UniscaleDemo/Messages/Messages/DirectMessageFull"

const initializeDispatcher = async (): Promise<DispatcherSession> => {
    const session = await Platform.builder()
      .withInterceptors(i => {
        i.interceptRequest(
            Patterns.messages.getDirectMessageList.allRequestUsages,
            Patterns.messages.getDirectMessageList.handleDirect((_input, _ctx) => {
              return [DirectMessageFull.samples().defaultSample()]
            })
        )
      })
      .build()

    return session
      .asSolution("fb344616-794e-4bd7-b81a-fb1e3361701f")
      .withLocale("en-GB")
      .withDataTenant("Customer 1 data tenant")
}
```



### Step 2: Call the endpoint

The endpoint now returns the mock data returned by your interceptor. When you have a working service, you can just remove the mock interceptor from your dispatcher.

```typescript
const messages = await dispatcher.request(GetDirectMessageList.with(userIdentifier))
```
