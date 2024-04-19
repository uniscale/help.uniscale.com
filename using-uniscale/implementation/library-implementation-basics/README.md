# Library implementation basics

### Prerequisites

{% hint style="info" %}
* You understand the architecture of the SDK
* You have generated an SDK and downloaded it with one of the supported package managers
* You are able to locate endpoints and contracts of the SDK  for imports
{% endhint %}

## Introduction

You now have the SDK at hand and you're wondering how to get started. To utilise your endpoints you can use the generated `Platform`. You will need to start by initializing a `PlatformSession` that will work as a base for your actions. Depending on the needs of your specific service, you will then use the session to initialize a dispatcher, create forwarding sessions, accept gateway requests etc.&#x20;

Our sessions come bundled with support for client-server usage and request forwarding tools for when you're working with multiple services at once. Interceptors make life easy for you defining exactly what needs to be implemented and what data you have in use. On top of that with pattern interceptors you can implement a bunch at a time. This gives you the opportunity to implement your authentication and transport mechanisms in a way that works for you.

You can use the library to test out and prototype your service interfaces ahead of building your service by using the generated sample data. When you have finished your implementation, you move from samples into proper implementations without having to change the interactions.

## Initialize session

To get started you will first have to create your `PlatformSession`. It will allow you to easily write handlers for your endpoints and interact with them as a user of your defined functionality. **Platform session is something you initialize once** and keep for the lifetime of your application.

{% tabs %}
{% tab title="C# .NET" %}
Starter for session initialisation. Create from builder and define interceptors.

{% code lineNumbers="true" fullWidth="true" %}
```csharp
using Uniscale.Designtime;

var session = await Platform.Builder()
   // Set up interceptors for the endpoints
   .WithInterceptors(i =>
   {
       // Implementation in later samples
   })
   // And build the session
   .Build();
```
{% endcode %}

While you can get started with just interceptors, the session initialization allows you to define more functionality on a general level.

{% code lineNumbers="true" %}
```csharp
using Uniscale.Designtime;

var session = await Platform.Builder()
    // Set up interceptors for the endpoints
    .WithInterceptors(i =>
    {
        // Implementation in later samples
    })
    // Define functionality for logging throughout
    .OnLogMessage(message => Console.WriteLine(message))
    // Inspect requested and returned objects
    .InspectRequests((o, ctx) => Console.WriteLine(o.ToString()))
    .InspectResponses((result, o, ctx) => Console.WriteLine(result.Value))
    // And build the session
    .Build();
```
{% endcode %}
{% endtab %}

{% tab title="Python" %}
Starter for session initialisation. Create from builder and define interceptors.

{% code lineNumbers="true" fullWidth="true" %}
```python
from uniscale.core.platform.platform import Platform

session = (
    await Platform.builder()
    # Set up an interceptors for the endpoints
    .with_interceptors(
        lambda i: i
        # Implementation in later samples
    ).build()
)
```
{% endcode %}

While you can get started with just interceptors, the session initialization allows you to define more functionality on a general level.

{% code lineNumbers="true" %}
```python
from uniscale.core.platform.platform import Platform

session = (
    await Platform.builder()
    # Set up an interceptors for the endpoints
    .with_interceptors(
        lambda i: i
        # Implementation in later samples
    )
    # Define functionality for logging throughout
    .on_log_message(lambda message: print(message))
    # Inspect requested and returned objects
    .inspect_requests(lambda o, ctx: print(o))
    .inspect_responses(lambda result, o, ctx: print(result.Value))
    # And build the session
    .build()
)
```
{% endcode %}
{% endtab %}

{% tab title="Java" %}
Starter for session initialisation. Create from builder and define interceptors.

{% code lineNumbers="true" fullWidth="true" %}
```java
import com.uniscale.sdk.Platform;

var session =
    Platform.builder()
        // Set up interceptors for the endpoints
        .withInterceptors(
            i -> {
              // Implementation in later samples
            })
        // And build the session
        .build()
        .join();
```
{% endcode %}

While you can get started with just interceptors, the session initialization allows you to define more functionality on general level.

{% code lineNumbers="true" %}
```java
using Uniscale.Designtime;

var session =
    Platform.builder()
        // Set up interceptors for the endpoints
        .withInterceptors(
            i -> {
              // Implementation in later samples
            })
        // Define functionality for logging throughout
        .onLogMessage(System.out::println)
        // Inspect requested and returned objects
        .inspectRequests((o, ctx) -> System.out.println(o.toString()))
        .inspectResponses((result, o, ctx) -> 
            System.out.println(result.getValue()))
        // And build the session
        .build()
        .join();
```
{% endcode %}
{% endtab %}

{% tab title="TypeScript" %}
Starter for session initialisation. Create from builder and define interceptors.

{% code lineNumbers="true" fullWidth="true" %}
```typescript
import { Platform } from "@uniscale-sdk/ActorCharacter-Messagethreads"

const session = await Platform.builder()
  // Set up interceptors for the endpoints
  .withInterceptors(i => {
    // Implementation in later samples
  })
  // And build the session
  .build()
```
{% endcode %}

While you can get started with just interceptors, the session initialization allows you to define more functionality on a general level.

{% code lineNumbers="true" %}
```typescript
import { Platform } from "@uniscale-sdk/ActorCharacter-Messagethreads"

const session = await Platform.builder()
  // Set up interceptors for the endpoints
  .withInterceptors(i => {
    // Implementation in later samples
  })
  // Define functionality for logging throughout
  .onLogMessage({ logLevel: 2, write: (message) => console.log(message) })
  // Inspect requested and returned objects
  .inspectRequests((input, _ctx) => {
    console.log(input.toString())
  })
  .inspectResponses((result, _input, _ctx) => {
    console.log(result.value)
  })
  // And build the session
  .build()
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Defining interceptors

Define the functionality of your endpoints inside the interceptors. You can intercept each function separately and have the data typed, or intercept whole namespaces and deal with untyped data.

Your interceptor's `handle` function has two parameters:

1. The input model defined for your endpoint
2. FeatureContext
   * This context will follow any request you make and contains the information about which solution, characters, language, data tenant and more this request was made with.

{% tabs %}
{% tab title="C# .NET" %}
In a typical situation you can write interceptors for each endpoint

{% code lineNumbers="true" fullWidth="true" %}
```csharp
using Uniscale.Designtime;
using UniscaleDemo.Account_1_0.Functionality.ServiceToModule.
    Account.Registration.ContinueToApplication;
using UniscaleDemo.Account.Account;
using UniscaleDemo.Messages;

var session = await Platform.Builder()
    // Set up interceptors for endpoints
    .WithInterceptors(i =>
    {
        i.InterceptRequest(
            GetOrRegister.AllFeatureUsages,
            GetOrRegister.Handle((input, ctx) =>
                Result<UserFull>.Ok(UserFull.Samples().DefaultSample())));
        
        // You can also intercept with patterns
        i.InterceptMessage(
            Patterns.Messages.SendMessage.AllMessageUsages,
            Patterns.Messages.SendMessage.Handle((input, ctx) =>
            {
                // You can validate and use defined error codes on return
                if (string.IsNullOrEmpty(input.Message))
                    return Result.BadRequest(
                        ErrorCodes.Messages.InvalidMessageLength);
                Console.WriteLine(
                    ctx.Characters.Performer?.Terminology == "Term.Admin"
                        ? $"Admin sent message: {input.Message}"
                        : $"{input.By} sent message: {input.Message}");
                return Result.Ok();
            }));
    })
    .Build();
```
{% endcode %}

\
However, there are some cases where it makes more sense to have one implementation for a group of endpoints, like for example in your frontend when calling a specific backend service for all endpoints under the messages namespace. We stay out of your way and **allow you to choose your preferred authentication and transport mechanisms**.

{% code lineNumbers="true" %}
```csharp
using Uniscale.Core;
using Uniscale.Designtime;
using UniscaleDemo.Messages;

var session = await Platform.Builder()
    .WithInterceptors(i =>
    {
        // We can intercept the whole messages namespace with a pattern
        i.InterceptPattern(Patterns.Messages.Pattern, async (input, ctx) =>
        {
            // By creating a GatewayRequest JSON, the receiving end can simply
            // handle incoming calls with session.AcceptGatewayRequest()
            var json = GatewayRequest.From(input, ctx).ToJson();
            var responseJson = await SendToMessageService(json);
            // Convert JSON return from AcceptGatewayRequest
            return Result<object>.FromJson(responseJson);
        });
        
        // You can also intercept all (remaining) calls to a general endpoint
        i.InterceptPattern("*", async (input, ctx) =>
        {
            var request = GatewayRequest.From(input, ctx);
            var responseJson = await CallGeneralServiceEndpoint(request);
            return Result<object>.FromJson(responseJson);
        });
    })
    .Build();
```
{% endcode %}
{% endtab %}

{% tab title="Python" %}
In typical situation you can write interceptors for each endpoint

{% code lineNumbers="true" fullWidth="true" %}
```python
from uniscale.core.platform.platform import Platform
from uniscale.core import Result
from uniscale.core.utilisation.utilisation_session_base import FeatureContext
from uniscale.uniscaledemo.account_1_0.functionality.servicetomodule.account.registration.continuetoapplication.get_or_register import GetOrRegister
from uniscale.uniscaledemo.account.account.user_full import UserFull
from uniscale.uniscaledemo.messages.messages.send_message_input import SendMessageInput
from uniscale.uniscaledemo.messages.patterns import Patterns
from uniscale.uniscaledemo.messages_1_0.error_codes import ErrorCodes


# Example for under message intercept lambda
def handle_send_message(
    cinput: SendMessageInput, ctx: FeatureContext
) -> Result:
    # You can validate and use defined error codes on return
    if not cinput.message:
        return Result.bad_request(ErrorCodes.messages.invalid_message_length)
    if ctx.characters.performer.terminology == "Term.Admin":
        print("Admin sent message: " + cinput.message)
    else:
        print(cinput.by + " sent message: " + cinput.message)
    return Result.ok(None)

session = (
    await Platform.builder()
    # Set up an interceptors for the endpoints
    .with_interceptors(
        lambda i: i.intercept_request(
            GetOrRegister.all_feature_usages,
            GetOrRegister.handle(
                lambda cinput, ctx: Result.ok(
                    UserFull.samples().default_sample()
                )
            ),
        # You can also intercept with patterns
        ).intercept_message(
            Patterns.messages.send_message.all_message_usages,
            Patterns.messages.send_message.handle(
                lambda cinput, ctx: handle_send_message
            ),
        )
    ).build()
)
```
{% endcode %}

\
However there are some cases where it makes more sense to have one implementation for group of endpoints, like for example in your frontend when calling specific backend service for all endpoints under the messages namespace. We stay out of your way and **allow you to choose your preferred authentication and transport mechanisms**.

{% code lineNumbers="true" %}
```python
from uniscale.core.platform.platform import Platform
from uniscale.core import Result, GatewayRequest
from uniscale.uniscaledemo.messages.patterns import Patterns


# Example for under message intercept lambda
async def gateway_message_interceptor(cinput, ctx) -> Result:
    # By creating GatewayRequest JSON, receiving end can simply
    # handle incoming call with session.accept_gateway_request()
    json = GatewayRequest.from_(cinput, ctx).to_json()
    response_json = await send_to_message_service(json)
    # Convert JSON return from accept_gateway_request
    result = Result.from_json(response_json)

    return result

# Example for under general intercept lambda
async def gateway_general_interceptor(cinput, ctx) -> Result:
    request = GatewayRequest.from_(cinput, ctx)
    response_json = await call_general_service_endpoint(request)
    result = Result.from_json(response_json)

    return result

session = (
    await Platform.builder()
    .with_interceptors(
        # We can intercept whole messages namespace with pattern
        lambda i: i.intercept_pattern(
            Patterns.messages.pattern,
            gateway_message_interceptor,

        # You can intercept all (remaining) calls to general endpoint
        ).intercept_pattern("*", gateway_general_interceptor)
    )
    .build()
)
```
{% endcode %}
{% endtab %}

{% tab title="Java" %}
In typical situation you can write interceptors for each endpoint

{% code lineNumbers="true" fullWidth="true" %}
```java
import com.uniscale.sdk.Platform;
import com.uniscale.sdk.core.Result;
import java.util.Objects;
import uniscaledemo.account.account.UserFull;
import uniscaledemo.account_1_0.functionality.servicetomodule.account.registration.continuetoapplication.GetOrRegister;
import uniscaledemo.messages.Patterns;
import uniscaledemo.messages_1_0.ErrorCodes;

var session =
    Platform.builder()
        // Set up an interceptors for features
        .withInterceptors(
            i -> {
              i.interceptRequest(
                  GetOrRegister.allFeatureUsages,
                  GetOrRegister.handle(
                      (input, ctx) -> Result.ok(UserFull.samples().defaultSample())));
    
              // You can also intercept with patterns
              i.interceptMessage(
                  Patterns.messages.sendMessage.allMessageUsages,
                  Patterns.messages.sendMessage.handle(
                      (input, ctx) -> {
                        // You can validate and use defined error codes on return
                        if (input.getMessage() == null || input.getMessage().isEmpty())
                          return Result.badRequest(ErrorCodes.messages.invalidMessageLength);
                        System.out.println(
                            Objects.equals(
                                    ctx.getCharacters().getPerformer().getTerminology(),
                                    "Term.Admin")
                                ? String.format("Admin sent message: %s", input.getMessage())
                                : String.format(
                                    "%s sent message: %s", input.getBy(), input.getMessage()));
                        return Result.ok();
                      }));
            })
        .build()
        .join();
```
{% endcode %}

\
However there are some cases where it makes more sense to have one implementation for group of endpoints, like for example in your frontend when calling specific backend service for all endpoints under the messages namespace. We stay out of your way and **allow you to choose your preferred authentication and transport mechanisms**.

<pre class="language-java" data-line-numbers><code class="lang-java">import com.uniscale.sdk.Platform;
import com.uniscale.sdk.core.GatewayRequest;
import com.uniscale.sdk.core.Result;
import java.util.concurrent.CompletableFuture;
import uniscaledemo.messages.Patterns;

<strong>var session =
</strong>  Platform.builder()
      .withInterceptors(
          i -> {
            // We can intercept whole messages namespace with pattern
            i.interceptPattern(
                Patterns.messages.getPattern(),
                (input, ctx) -> {
                  // By creating GatewayRequest JSON, receiving end can simply
                  // handle incoming call with session.acceptGatewayRequest()
                  var json = GatewayRequest.from(input, ctx).toJson();
                  var responseJson = sendToMessageService(json);
                  // Convert JSON return from acceptGatewayRequest
                  return CompletableFuture.completedFuture(Result.fromJson(responseJson));
                });
  
            // You can also intercept all (remaining) calls to general endpoint
            i.interceptPattern(
                "*",
                (input, ctx) -> {
                  var request = GatewayRequest.from(input, ctx);
                  var responseJson = callGeneralServiceEndpoint(request);
                  return CompletableFuture.completedFuture(Result.fromJson(responseJson));
                });
          })
      .build()
      .join();
</code></pre>
{% endtab %}

{% tab title="TypeScript" %}
In typical situation you can write interceptors for each endpoint

{% code lineNumbers="true" fullWidth="true" %}
```typescript
import { Platform, Result } from "@uniscale-sdk/ActorCharacter-Messagethreads"
import { Patterns as MessagePatterns } from "@uniscale-sdk/ActorCharacter-Messagethreads/sdk/UniscaleDemo/Messages"
import { GetOrRegister } from "@uniscale-sdk/ActorCharacter-Messagethreads/sdk/UniscaleDemo/Account_1_0/Functionality/ServiceToModule/Account/Registration/ContinueToApplication"
import { UserFull } from "@uniscale-sdk/ActorCharacter-Messagethreads/sdk/UniscaleDemo/Account/Account/UserFull"
import { ErrorCodes } from "@uniscale-sdk/ActorCharacter-Messagethreads/sdk/UniscaleDemo/Messages_1_0"

const session = await Platform.builder()
  // Set up interceptors for the endpoints
  .withInterceptors((i) => {
    i.interceptRequest(
      GetOrRegister.allFeatureUsages,
      GetOrRegister.handle((_input, _ctx) => {
        return Result.ok(UserFull.samples().defaultSample())
      }),
    )
    // You can also intercept with patterns
    i.interceptMessage(
      MessagePatterns.messages.sendMessage.allMessageUsages,
      MessagePatterns.messages.sendMessage.handle((input, ctx) => {
        // You can validate and use defined error codes on return
        if (!input.message) {
          return Result.badRequest(ErrorCodes.messages.invalidMessageLength)
        }
        console.log(
          ctx.characters.performer?.terminology === "Term.Admin"
            ? `Admin sent a message: ${input.message}`
            : `${input.by} sent a message: ${input.message}`,
        );
        return Result.ok(undefined)
      }),
    );
  })
  .build()
```
{% endcode %}

\
However there are some cases where it makes more sense to have one implementation for group of endpoints, like for example in your frontend when calling specific backend service for all endpoints under the messages namespace. We stay out of your way and **allow you to choose your preferred authentication and transport mechanisms**.

{% code lineNumbers="true" %}
```typescript
import { GatewayRequest, Platform, Result } from "@uniscale-sdk/ActorCharacter-Messagethreads"
import { Patterns as MessagePatterns } from "@uniscale-sdk/ActorCharacter-Messagethreads/sdk/UniscaleDemo/Messages"

const session = await Platform.builder()
  .withInterceptors((i) => {
    i.interceptPattern(MessagePatterns.messages.pattern, async (input, ctx) => {
      // By creating GatewayRequest JSON, the receiving end can simply
      // handle incoming call with session.acceptGatewayRequest()
      const json = GatewayRequest.from(input, ctx).toJson()
      const responseJson = await sendToMessageService(json)
      // The response needs to be serialized into the Result class
      return Result.fromJson(responseJson)
    })
    // You can also intercept all (remaining) calls to a general endpoint
    i.interceptPattern("*", async (input, ctx) => {
      const request = GatewayRequest.from(input, ctx)
      const responseJson = await callGeneralServiceEndpoint(request)
      return Result.fromJson(responseJson)
    })
  })
  .build()
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Handle endpoints and make requests

With the platform session you have a setup that knows how to handle your endpoints. To utilise that and call your endpoints you need to get a `DispatcherSession` through which you can interact with your endpoints. Dispatchers are designed to be set up in a way where _one_ dispatcher can handle all your solution/service's endpoints.

{% hint style="info" %}
Making a request: PlatformSession -> DispatcherSession -> Request()
{% endhint %}

Platform session can also be used to receive requests. If in your endpoint you can turn your data into a GatewayRequest (or you sent the data with our helpers), you use AcceptGatewayRequest in your session and let the platform handle the request based on your interceptor implementations.

{% hint style="info" %}
Receiving a request: PlatformSession -> AcceptGatewayRequest()
{% endhint %}

{% tabs %}
{% tab title="C# .NET" %}
The typical case for making a request and creating a GatewayRequest from it.

{% code lineNumbers="true" fullWidth="true" %}
```csharp
using Uniscale.Core;
using Uniscale.Designtime;
using UniscaleDemo.Account_1_0.Functionality.ServiceToModule.
    Account.Registration.ContinueToApplication;

var session = await Platform.Builder()
    // Set up your PlatformSession as in above samples
    // For example sending all to GeneralServiceEndpoint
    .WithInterceptors(i =>
    {
        i.InterceptPattern("*", async (input, ctx) =>
        {
            var request = GatewayRequest.From(input, ctx);
            var responseJson = await CallGeneralServiceEndpoint(request);
            return Result<object>.FromJson(responseJson);
        });
    })
    .Build();

// Initialize a DispatcherSession with a solution id of your choice
var dispatcher = session
    .AsSolution(Guid.Parse("a18b2b3e-4010-4c0f-a01f-565fda8c466e"));

// Create a new user and check if we got a successful response
var result = await dispatcher
    .Request(GetOrRegister.With("myAwesomeUserHandle"));
if (result.Success)
    Console.WriteLine(
        "User: id=" + result.Value.UserIdentifier +
        " Handle=" + result.Value.Handle);
else
    Console.WriteLine("Failed with: " + result.Error.ToLongString());
```
{% endcode %}

And a quick sample on how one would receive such request.

<pre class="language-csharp" data-line-numbers><code class="lang-csharp"><strong>using Uniscale.Core;
</strong>using UniscaleDemo.Account_1_0.Functionality.ServiceToModule.
    Account.Registration.ContinueToApplication;
using UniscaleDemo.Account.Account;

var session = await Platform.Builder()
    // Implement what happens on endpoints when GatewayRequests come in.
    .WithInterceptors(i => i
        .InterceptRequest(
            GetOrRegister.AllFeatureUsages,
            GetOrRegister.Handle((input, ctx) =>
                Result&#x3C;UserFull>.Ok(UserFull.Samples().DefaultSample()))))
    .Build();


// In your endpoint handler (Http endpoint or similar)
var result = await session.AcceptGatewayRequest(requestJson);
return result.ToJson();
</code></pre>
{% endtab %}

{% tab title="Python" %}
The typical case for creating a request and creating a GatewayRequest from it.

{% code lineNumbers="true" fullWidth="true" %}
```python
from uuid import UUID
from uniscale.core.platform.platform import Platform
from uniscale.core import Result, GatewayRequest
from uniscale.uniscaledemo.account_1_0.functionality.servicetomodule.account.registration.continuetoapplication.get_or_register import GetOrRegister


# Example for under general intercept lambda
async def gateway_general_interceptor(cinput, ctx) -> Result:
    request = GatewayRequest.from_(cinput, ctx)
    response_json = await call_general_service_endpoint(request)
    result = Result.from_json(response_json)

    return result

session = (
    await Platform.builder()
    # Set up your PlatformSession as in above samples
    # For example sending all to GeneralServiceEndpoint
    .with_interceptors(
        lambda i: i.intercept_pattern("*", gateway_general_interceptor)
    ).build()
)

# Initialize a DispatcherSession with a solution id of your choice
dispatcher = session.as_solution(UUID("a18b2b3e-4010-4c0f-a01f-565fda8c466e"))

# Create a new user and check if we got a successful response
result = await dispatcher.request(GetOrRegister.with_("myAwesomeUserHandle"))
if result.is_success():
    print(
        "User: id="
        + str(result.value.user_identifier)
        + " Handle="
        + result.value.handle
    )
else:
    print("Failed with: " + result.error.to_long_string())
```
{% endcode %}

And a quick sample on how one would receive such request.

{% code lineNumbers="true" %}
```python
from uniscale.core.platform.platform import Platform
from uniscale.core import Result, GatewayRequest
from uniscale.uniscaledemo.account_1_0.functionality.servicetomodule.account.registration.continuetoapplication.get_or_register import GetOrRegister
from uniscale.uniscaledemo.account.account.user_full import UserFull


session = (
    await Platform.builder()
    # Implement what happens on endpoints when GatewayRequests come in.
    .with_interceptors(
        lambda i: i.intercept_request(
            GetOrRegister.all_feature_usages,
            GetOrRegister.handle(
                lambda cinput, ctx: Result.ok(
                    UserFull.samples().default_sample()
                )
            )
        )
    ).build()
)


# In your endpoint handler (Http endpoint or similar)
result = await session.accept_gateway_request(request_json)
return result.to_json()
```
{% endcode %}
{% endtab %}

{% tab title="Java" %}
The typical case for creating a request and creating a GatewayRequest from it.

{% code lineNumbers="true" fullWidth="true" %}
```java
import com.uniscale.sdk.Platform;
import com.uniscale.sdk.core.GatewayRequest;
import com.uniscale.sdk.core.Result;
import java.util.UUID;
import java.util.concurrent.CompletableFuture;
import uniscaledemo.account_1_0.functionality.servicetomodule.
    account.registration.continuetoapplication.GetOrRegister;

var session =
    Platform.builder()
        // Set up your PlatformSession as in above samples
        // For example sending all to GeneralServiceEndpoint
        .withInterceptors(
            i -> {
              i.interceptPattern(
                  "*",
                  (input, ctx) -> {
                    var request = GatewayRequest.from(input, ctx);
                    var responseJson = callGeneralServiceEndpoint(request);
                    return CompletableFuture.completedFuture(
                        Result.fromJson(responseJson));
                  });
            })
        .build()
        .join();

// Initialize a DispatcherSession with a solution id of your choice
var dispatcher = session.asSolution(
    UUID.fromString("a18b2b3e-4010-4c0f-a01f-565fda8c466e"));

// Create a new user and check if we got a successful response
var result = dispatcher.request(GetOrRegister.with("myAwesomeUserHandle"))
    .join();
if (result.isSuccess())
  System.out.printf(
      "User: id= %s Handle= %s%n",
      result.getValue().getUserIdentifier(), result.getValue().getHandle());
else System.out.printf("Failed with: %s%n", result.getError().toLongString());
```
{% endcode %}

And a quick sample on how one would receive such request.

{% code lineNumbers="true" %}
```java
import com.uniscale.sdk.Platform;
import com.uniscale.sdk.core.Result;
import uniscaledemo.account.account.UserFull;
import uniscaledemo.account_1_0.functionality.servicetomodule.
    account.registration.continuetoapplication.GetOrRegister;

var session =
    Platform.builder()
        // Implement what happens on endpoints when GatewayRequests come in.
        .withInterceptors(
            i ->
                i.interceptRequest(
                    GetOrRegister.allFeatureUsages,
                    GetOrRegister.handle(
                        (input, ctx) -> Result.ok(UserFull.samples().defaultSample()))))
        .build()
        .join();

// In your endpoint handler (Http endpoint or similar)
var result = session.acceptGatewayRequest(requestJson).join();
return result.toJson();
```
{% endcode %}
{% endtab %}

{% tab title="TypeScript" %}
The typical case for creating a request and creating a GatewayRequest from it.

{% code lineNumbers="true" fullWidth="true" %}
```typescript
import { GatewayRequest, Platform, Result } from "@uniscale-sdk/ActorCharacter-Messagethreads"
import { GetOrRegister } from "@uniscale-sdk/ActorCharacter-Messagethreads/sdk/UniscaleDemo/Account_1_0/Functionality/ServiceToModule/Account/Registration/ContinueToApplication"

const session = await Platform.builder()
  .withInterceptors((i) => {
    // Set up your PlatformSession as in above samples
    // For example sending all to GeneralServiceEndpoint
    i.interceptPattern("*", async (input, ctx) => {
      const request = GatewayRequest.from(input, ctx)
      const responseJson = callGeneralServiceEndpoint(request)
      return Result.fromJson(responseJson)
    })
  })
  .build()

// Initialize a DispatcherSession with a solution id of your choice
const dispatcher = session.asSolution('fb344616-794e-4bd7-b81a-fb1e3361701f')

// Create a new user and check if we got a successful response
const result = await dispatcher.request(GetOrRegister.with('myAwesomeUserHandle'))

if (result.success) {
  console.log(`User: id=${result.value?.identifier}`)
  return
}
console.log(`Failed with: ${result.error?.toLongString()}`)
```
{% endcode %}

And a quick sample on how one would receive such request.

{% code lineNumbers="true" %}
```typescript
import { Platform, Result, BackendAction } from "@uniscale-sdk/ActorCharacter-Messagethreads"
import { GetOrRegister } from "@uniscale-sdk/ActorCharacter-Messagethreads/sdk/UniscaleDemo/Account_1_0/Functionality/ServiceToModule/Account/Registration/ContinueToApplication"
import { UserFull } from "@uniscale-sdk/ActorCharacter-Messagethreads/sdk/UniscaleDemo/Account/Account/UserFull"

const session = await Platform.builder()
  // Implement what happens on endpoints when GatewayRequests come in
  .withInterceptors((i) => {
    i.interceptRequest(
      GetOrRegister.allFeatureUsages,
      GetOrRegister.handle((_input, _ctx) => {
        return Result.ok(UserFull.samples().defaultSample())
      }),
    )
  })
  .build()


// In your endpoint handler (Http endpoint or similar)
const result = await session.acceptGatewayRequest(requestJson)
return result.toJson()

```
{% endcode %}
{% endtab %}
{% endtabs %}

You can use the created dispatcher to make multiple requests and fetch Terminologies that you have defined into your model. You can find a more complex sample of how forwarding works in [forwarding-session-basics.md](forwarding-session-basics.md "mention").

***

## Conclusion

This tutorial has information on everything you need to consider when getting started with your minimalistic implementation. If you want to see all of it come together, you can find samples based on our Demo solution in: [https://github.com/uniscale?q=demo-](https://github.com/uniscale?q=demo-).  You can test it out, mix and match frontend and backend demos as you want.
