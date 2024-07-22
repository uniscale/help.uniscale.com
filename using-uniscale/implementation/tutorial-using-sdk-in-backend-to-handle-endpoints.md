---
description: Learn how to use the SDK in your backend to handle endpoints.
---

# Tutorial: Using SDK in backend to handle endpoints

On this page, you will learn how to use the SDK with your back-end application. The tutorial uses Uniscale's Message Threads demo solution as its base. For more detailed information on the SDK, see [library-implementation-basics](library-implementation-basics/ "mention").

You can find similar complete code samples with running instructions in our GitHub for every language:

* [https://github.com/uniscale/demo-net-backend](https://github.com/uniscale/demo-net-backend)
* [https://github.com/uniscale/demo-python-backend](https://github.com/uniscale/demo-python-backend)
* [https://github.com/uniscale/demo-java-backend](https://github.com/uniscale/demo-java-backend)
* [https://github.com/uniscale/demo-ts-backend](https://github.com/uniscale/demo-ts-backend)



## SDK Installation

You can find a guide with correct SDK information for your generated languages in your solution or service's SDK Portal in Uniscale.



## Implementing the endpoint logic

Your SDK is built with the endpoints that you have defined.  In order to get started with your backend you will need to implement the logic of the endpoint and create an interceptor for it that you register inside `PlatformSession`.&#x20;

In this sample, we will implement basic logic for `GetOrRegister` the endpoint. This endpoint will simply return the pre-generated sample data for return type. We then register that interceptor into an instance of a session, which can be injected/passed to our endpoint/controller.

{% tabs %}
{% tab title="C# .NET" %}
For example, if we create ASP.NET Core WebAPI. We will need to add PlatformSession into services when building the `WebApplication`.

{% code title="Program.cs" %}
```csharp
using Uniscale.Core;
using Uniscale.Designtime;
using UniscaleDemo.Account_1_0.Functionality.ServiceToModule.Account.Registration.ContinueToApplication;
using UniscaleDemo.Account.Account;

var builder = WebApplication.CreateBuilder(args);

// Add services to the container.
builder.Services.AddSingleton<PlatformSession>(_ =>
{
    return Platform.Builder()
        // Implement what happens on endpoints when GatewayRequests come in.
        .WithInterceptors(i => i
            .InterceptRequest(
                GetOrRegister.AllFeatureUsages,
                GetOrRegister.Handle((input, ctx) =>
                    Result<UserFull>.Ok(UserFull.Samples().DefaultSample()))))
        .Build()
        .Result;
});

// ... Rest of your basic .NET scaffold / Initialize code

```
{% endcode %}
{% endtab %}

{% tab title="Python" %}
For example, creating a simple Quart backend app. We will need to initialize the Quart app and setup the PlatformSession with our interceptor logic before serving.

{% code title="app.py" %}
```python
from typing import Optional
from quart import Quart, request
from quart_cors import cors

from uniscale.core import (
    Result,
    PlatformSession,
)
from uniscale.core.platform.platform import Platform
from uniscale.uniscaledemo.account_1_0.functionality.servicetomodule.account.registration.continuetoapplication.get_or_register import (
    GetOrRegister,
)
from uniscale.uniscaledemo.account.account.user_full import UserFull


# Initialize Quart app.
app = Quart(__name__)
app = cors(app, allow_origin="*")

# Define instances for builder and PlatformSession
builder = Platform.builder()
session: Optional[PlatformSession] = None

#initialize session with interceptors and other logic before serving
@app.before_serving
async def setup_session():
    global session

    session = await builder.with_interceptors(
        lambda i: i.intercept_request(
            GetOrRegister.all_feature_usages,
            GetOrRegister.handle(
                lambda cinput, ctx: Result.ok(UserFull.samples().default_sample())
            ),
        )
    ).build()

# endpoint and app start in next sample
```
{% endcode %}
{% endtab %}

{% tab title="Java" %}
For example, if we were creating spring boot app with the web starter.

{% code title="pom.xml" %}
```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```
{% endcode %}

You can initialize the Spring Boot application like you usually do. We will create a Bean of PlatformSession with the interceptor logic implemented.

{% code title="DemoApplication.java" %}
```java
package com.example.demo;

import com.uniscale.sdk.Platform;
import com.uniscale.sdk.core.PlatformSession;
import com.uniscale.sdk.core.Result;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.context.annotation.Bean;
import uniscaledemo.account.account.UserFull;
import uniscaledemo.account_1_0.functionality.servicetomodule
  .account.registration.continuetoapplication.GetOrRegister;

@SpringBootApplication
public class DemoApplication {
  public static void main(String[] args) {
    SpringApplication.run(DemoApplication.class, args);
  }

  @Bean
  public PlatformSession platformSession() {
    return Platform.builder()
        .withInterceptors(
            i ->
                i.interceptRequest(
                    GetOrRegister.allFeatureUsages,
                    GetOrRegister.handle(
                        (input, ctx) -> Result.ok(UserFull.samples()
                          .defaultSample()))))
        .build()
        .join();
  }
}

```
{% endcode %}
{% endtab %}

{% tab title="TypeScript" %}
For example, if we create an express backend web application. First we export a PlatformSession and create initialized function for it.

```typescript
import express from "express"
import cors from "cors"
import {
  BackendAction,
  Platform,
  PlatformSession,
  Result,
} from "@uniscale-sdk/ActorCharacter-Messagethreads"
import { GetOrRegister } from "@uniscale-sdk/ActorCharacter-Messagethreads/sdk/UniscaleDemo/Account_1_0/Functionality/ServiceToModule/Account/Registration/ContinueToApplication"
import { UserFull } from "@uniscale-sdk/ActorCharacter-Messagethreads/sdk/UniscaleDemo/Account/Account"

// Prepare PlatformSession for our endpoint
export let platformSession: PlatformSession

export const initializePlatformSession = async () => {
  platformSession = await Platform.builder()
    .withInterceptors((i) => {
      i.interceptRequest(
        GetOrRegister.allFeatureUsages,
        GetOrRegister.handle((_input, _ctx) => {
          return Result.ok(UserFull.samples().defaultSample())
        }),
      )
    })
    .build()
}

```

We will then initialize the express application. We will need to initialize the PlatformSession on startup and ensure it's usable in endpoints alter on.

```typescript
// Start express server as you see fit. 
export const startServer = () => {
  const PORT = 7156
  const app = express()

  app.use(express.json())
  app.use(cors())

  // Endpoint comes here from next sample

  app.listen(PORT, () => {
    console.log(`Server is listening on port ${PORT}`)
  })
}

// On startup you will need to initialize the session with interceptors
const app = async () => {
  await initializePlatformSession()
  startServer()
}

app()
```
{% endtab %}
{% endtabs %}

Now there is a server running with PlatformSession ready to be injected/passed.



## Create network endpoint

With the server running and SDK endpoint logic implemented into your session, you're still missing the network endpoint. You will only need to be able to inject/pass an instance of PlatformSession into your controller/ network endpoint definition. Then inside your network endpoint, you need to pass the GatewayRequest JSON data into the session's acceptGatewayRequest function and return the output of that function in JSON.&#x20;

{% hint style="warning" %}
Use the `.toJson` function of `Result` to avoid any serialization issues.
{% endhint %}

These endpoints can be created using any library or protocol that fits your needs. You'll just need to be able to pass the content. We will select a library for each language and showcase an example, but this does not mean it would only work with these showcased techniques.

{% tabs %}
{% tab title="C# .NET" %}
For basic ASP.NET WebAPI, this means injecting the PlatformSession into your controller and creating a single HTTP endpoint that serves the app based on the created instance of PlatformSession.

{% code title="GatewayController.cs" %}
```csharp
using System.Text.Json;
using Microsoft.AspNetCore.Mvc;
using Uniscale.Core;

// Sample implementation for demo. Please note that this is just one showcase
// You are free to use your own protocols/libraries for this task.
namespace DemoApi.Controllers;

[ApiController]
[Route("")]
public class GatewayController : ControllerBase
{
    // Inject the PlatformSession into your controller
    private readonly PlatformSession _session;
    
    public GatewayController(PlatformSession session)
    {
        _session = session;
    }
    
    [HttpPost]
    public async Task<string> Handle([FromBody]JsonElement request)
    {
        // All you need to do is pass json to session and parse result to json.
        var result = await _session.AcceptGatewayRequest(request.GetRawText());
        return result.ToJson();
    }
}
```
{% endcode %}
{% endtab %}

{% tab title="Python" %}
For our Quart app, this means defining the single endpoint route using the PlatformSession. And then simply starting the app.

{% code title="app.py" %}
```python
# Sample implementation for demo. Please note that this is just one showcase
# You are free to use your own protocols/libraries for this task.

@app.route("/", methods=["POST"])
async def handle_request():
    # All you need to do is pass json to session and parse result to json.
    data = await request.get_data()
    result = await session.accept_gateway_request(data)
    return result.to_json()


if __name__ == "__main__":
    app.run(port=7156)

```
{% endcode %}
{% endtab %}

{% tab title="Java" %}
For basic Spring Boot API, this means injecting the PlatformSession into your controller and creating a single HTTP endpoint that serves the app based on the created instance of PlatformSession.

{% code title="GatewayController.java" %}
```java
package com.example.demo;

import com.uniscale.sdk.core.PlatformSession;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.ResponseBody;

// Sample implementation for demo. Please note that this is just one showcase
// You are free to use your own protocols/libraries for this task.

@Controller
public class GatewayController {
  private final PlatformSession session;

  public GatewayController(PlatformSession session) {
    this.session = session;
  }

  @PostMapping("")
  @ResponseBody
  public String handle(@RequestBody String request) {
    // All you need to do is pass json to session and parse result to json.
    return this.session.acceptGatewayRequest(request).join().toJson();
  }
}

```
{% endcode %}
{% endtab %}

{% tab title="TypeScript" %}
For basic express API, this means matching all routes and creating a single HTTP endpoint that serves the app based on the created instance of PlatformSession.

```typescript
// Sample implementation for demo. Please note that this is just one showcase
// You are free to use your own protocols/libraries for this task.

app.all("/", async (req, res) => {
  const request = req.body as BackendAction<unknown, unknown>
  // All you need to do is pass json to session and parse result to json.
  try {
    const value = await platformSession.acceptGatewayRequest(
      JSON.stringify(request),
    )
    res.status(200).send(value.toJson())
  } catch (error) {
    console.error(error)
    res.status(500).send(error)
  }
})
```
{% endtab %}
{% endtabs %}

With just a couple of steps like that, we have created a backend that can be easily called with a front-end client that was created based on [quick-start-front-end-with-uniscale-sdk](quick-start-front-end-with-uniscale-sdk/ "mention").
