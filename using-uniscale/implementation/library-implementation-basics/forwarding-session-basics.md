---
description: Learn the basics of forwarding sessions.
---

# Forwarding session basics

Real-world applications often need to call another service from the initial one that is called. We have created `ForwardingSession` to make this easier. Forwarding session-related tools help you with handling context, errors, and following transactions. Below is a sample where we have `clientSession` that is used to create a request into `registerServiceSession` which in turn creates a `ForwardingSession` and calls `messageServiceSession`.&#x20;



### Creating a sample in stages

Let's go through the flow, starting from the `clientSession`. We want to register a new user with the handle "AwesomeUserHandle". First, we create a pattern interceptor that sends a request to our account service, initialize the dispatcher, and make a request.

{% tabs %}
{% tab title="C# .NET" %}
{% code fullWidth="true" %}
```csharp
// Create the client session with pattern interceptor
var clientSession = await Platform.Builder()
    .WithInterceptors(i => i
        .InterceptPattern(UniscaleDemo.Account.Patterns.Pattern, 
            async (input, ctx) =>
            {
                var requestJson = GatewayRequest.From(input, ctx).ToJson();
                // This call should end up in AcceptGatewayRequest of the account
                // session that we create in a later sample.
                var response = await SendToAccountService(requestJson);
                return response;
            }))
    .Build();

var dispatcher = clientSession.AsSolution(
    // This Guid is the id of your solution.
    Guid.Parse("ac43912b-50cf-439a-9652-b378b197d80a"));

// Make the call to create a new user
var createdUser = await dispatcher.Request(
    GetOrRegister.With("AwesomeUserHandle"));
Console.WriteLine(createdUser.Success
    ? $"We created user with id: {createdUser.Value.UserIdentifier}"
    : createdUser.Error.ToLongString());
```
{% endcode %}
{% endtab %}

{% tab title="Python" %}
```python
# Handler for intercepting account pattern.
async def account_handler(cinput, ctx) -> Result:
    request_json = GatewayRequest.from_(cinput, ctx).to_json()
    # This call should end up in acceptGatewayRequest of the account.
    # session that we create in a later sample.
    response = await send_to_account_service(request_json)
    return response

# Create the client session with pattern interceptor
client_session = (
    await Platform.builder()
    .with_interceptors(
        lambda i: i.intercept_pattern(AccountPatterns.pattern, account_handler)
    )
    .build()
)

dispatcher = client_session.as_solution(
    # This uuid is the id of your solution.
    uuid.UUID("ac43912b-50cf-439a-9652-b378b197d80a")
)

# Make the call to create a new user
created_user = await dispatcher.request(
    GetOrRegister.with_("AwesomeUserHandle")
)
if created_user.is_success():
    print(f"We created user with id: {created_user.value.user_identifier}")
else:
    print(created_user.error.to_long_string())
```
{% endtab %}

{% tab title="Java" %}
```java
// Create the client session with pattern interceptor
var clientSession =
    Platform.builder()
        .withInterceptors(
            i ->
                i.interceptPattern(
                    uniscaledemo.account.Patterns.pattern,
                    (input, ctx) -> {
                      var requestJson = GatewayRequest.from(input, ctx)
                          .toJson();
                      // This call should end up in acceptGatewayRequest of 
                      // the account session that we create in a later sample.
                      var response = await sendToAccountService(requestJson);
                      return response;
                    }))
        .build()
        .join();

var dispatcher =
    clientSession.asSolution(
        // This uuid is the id of your solution.
        UUID.fromString("ac43912b-50cf-439a-9652-b378b197d80a"));

// Make the call to create a new user
var createdUser = dispatcher
    .request(GetOrRegister.with("AwesomeUserHandle"))
    .join();

if (createdUser.isSuccess())
  System.out.printf(
      "We created user with id: %s.%n",
      createdUser.getValue().getUserIdentifier());
else
  System.out.println(createdUser.getError().toLongString());
```
{% endtab %}

{% tab title="TypeScript" %}
```typescript
// Create the client session with pattern interceptor
const clientSession = await Platform.builder()
  .withInterceptors((i) =>
    i.interceptPattern(
      UniscaleDemoAccount.Patterns.pattern,
      async (input, ctx) => {
        const requestJson = GatewayRequest.from(input, ctx).toJson()
        // This call should end up in acceptGatewayRequest of the account
        // session that we create in a later sample.
        const response = await sendToAccountService(requestJson);
        return response
      },
    ),
  )
  .build()

const dispatcher = clientSession.asSolution(
  // This uuid is the id of your solution.
  "ac43912b-50cf-439a-9652-b378b197d80a",
)

// Make the call to create a new user
const createdUser = await dispatcher.request(
  GetOrRegister.with("AwesomeUserHandle"),
)
if (createdUser.isSuccess())
  console.log(
    `We created user with id: ${createdUser.value?.userIdentifier}`,
  )
else console.log(createdUser.error?.toLongString())
```
{% endtab %}
{% endtabs %}



`accountServiceSession` receives the client's request. We know that our account service will need to be forwarding the call on top of receiving it, so we will need separate sessions for each. The builder for the session which is forwarding calls to a message service (`messageForwardingSessionBuilder`) is created separately and can be reused if needed. Then in `accountServiceSession` we create the user, create a dispatcher based on `messageForwardingSessionBuilder` and make a request to message service.&#x20;

{% tabs %}
{% tab title="C# .NET" %}
{% code fullWidth="true" %}
```csharp
// Initialize builder for forwarding and service sessions, keep them linked.
var sessionBuilder = Platform.Builder();

// Prepare for outgoing message calls from the account service
var messageForwardingSessionBuilder = await sessionBuilder
    .ForwardingSessionBuilder(
        // This Guid is the service id of your message service.
        Guid.Parse("60888f37-1665-416e-a70f-09332a24f7bd"))
    .WithInterceptors(i => i
        .InterceptPattern(UniscaleDemo.Messages.Patterns.Pattern, 
            async (input, ctx) =>
            {
                var requestJson = GatewayRequest.From(input, ctx).ToJson();
                // This call should end up in AcceptGatewayRequest of the message
                // session that we create in a later sample.
                var response = await SendToMessageService(requestJson);
                return response;
            }))
    .Build();

var accountServiceSession = await sessionBuilder
    .WithInterceptors(i => i
        .InterceptRequest(
            GetOrRegister.AllFeatureUsages,
            GetOrRegister.Handle(async (input, ctx) =>
                {
                    // For demo, we'll create a sample user as a variable.
                    var created = new UserFull
                    {
                        Handle = input,
                        UserIdentifier = Guid.NewGuid()
                    };

                    // Request message service to celebrate new user.
                    var message = $"we registered {created.Handle}";
                    var dispatcher = await messageForwardingSessionBuilder
                        .ForTransaction(ctx.TransactionId);
                    var sendResult = await dispatcher.Request(
                        WelcomeUser.With(new WelcomeUserInput
                        {
                            // For demo the created user is the message sender.
                            WelcomedUser = new UserTag
                            {
                                By = created.UserIdentifier, 
                                At = DateTime.Now
                            },
                            Message = message
                        }));
                    if (!sendResult.Success)
                        return Result<UserFull>.InternalServerError(
                            "Demo.GeneralError",
                            $"Failed calling feature: {nameof(WelcomeUser)}");

                    // Response
                    return Result<UserFull>.Ok(created);
                }
            )))
    .Build();


// The endpoint of SendToAccountService.
var response = accountServiceSession.AcceptGatewayRequest(requestJson);
```
{% endcode %}
{% endtab %}

{% tab title="Python" %}
```python
# Initialize builder for forwarding and service sessions, keep them linked.
session_builder = Platform.builder()

async def message_handler(cinput, ctx) -> Result:
    request_json = GatewayRequest.from_(cinput, ctx).to_json()
    # This call should end up in acceptGatewayRequest of the message
    # session that we create in a later sample.
    response = await send_to_message_service(request_json)
    return response

# Prepare for outgoing message calls from the account service
message_forwarding_session_builder = (
    await session_builder.forwarding_session_builder(
        # This uuid is the service id of your message service.
        uuid.UUID("60888f37-1665-416e-a70f-09332a24f7bd")
    )
    .with_interceptors(
        lambda i: i.intercept_pattern(MessagePatterns.pattern, message_handler)
    )
    .build()
)

async def handle_get_or_register(cinput: str, ctx: FeatureContext) -> Result:
    # For demo, we'll create a sample user as a variable.
    created = UserFull(handle=cinput, user_identifier=uuid.uuid4())

    # Request message service to celebrate new user.
    message = f"we registered {created.handle}"
    dispatcher = await message_forwarding_session_builder.for_transaction(
        ctx.transaction_id
    )

    send_result = await dispatcher.request(
        WelcomeUser.with_(
            WelcomeUserInput(
                message=message,
                welcomed_user=UserTag(
                    by=created.user_identifier, at=datetime.now()
                ),
            )
        )
    )
    if not send_result.is_success():
        return Result.internal_server_error(
            "Demo.GeneralError", "Failed calling message service: SendMessage"
        )
    # Success response
    return Result.ok(created)

# Handle incoming calls for the account service
account_service_session = await session_builder.with_interceptors(
    lambda i: i.intercept_request(
        GetOrRegister.all_feature_usages,
        GetOrRegister.handle_async(handle_get_or_register),
    )
).build()


# The endpoint of SendToAccountService.
response = await account_service_session.accept_gateway_request(
    request_json
)
```
{% endtab %}

{% tab title="Java" %}
```java
// Initialize builder for forwarding and service sessions, keep them linked.
var sessionBuilder = Platform.builder();

// Prepare for outgoing message calls from the account service
var messageForwardingSessionBuilder =
    sessionBuilder
        .forwardingSessionBuilder(
            // This uuid is the service id of your message service.
            UUID.fromString("60888f37-1665-416e-a70f-09332a24f7bd"))
        .withInterceptors(
            i ->
                i.interceptPattern(
                    uniscaledemo.messages.Patterns.pattern,
                    (input, ctx) -> {
                      var requestJson = GatewayRequest.from(input, ctx)
                          .toJson();
                      // This call should end up in acceptGatewayRequest of 
                      // the message session that we create in a later sample.
                      var response = await sendToMessageService(requestJson);
                      return response;
                    }))
        .build()
        .join();

// Handle incoming calls for the account service
var accountServiceSession =
    sessionBuilder
        .withInterceptors(
            i ->
                i.interceptRequest(
                    GetOrRegister.allFeatureUsages,
                    GetOrRegister.handle(
                        (input, ctx) -> {
                          // For demo, we'll create a sample user as a variable.
                          var created =
                              UserFull.builder()
                                  .handle(input)
                                  .userIdentifier(UUID.randomUUID())
                                  .build();

                          // Request message service to celebrate new user.
                          var message = String.format("we registered %s.%n", 
                              created.getHandle());
                          var dispatcher =
                              messageForwardingSessionBuilder
                                  .forTransaction(ctx.getTransactionId())
                                  .join();
                          var sendResult =
                              dispatcher
                                  .request(
                                      // For demo the created user is sender.
                                      WelcomeUser.with(
                                          WelcomeUserInput.builder()
                                              .message(message)
                                              .welcomedUser(
                                                  UserTag.builder()
                                                      .by(created
                                                          .getUserIdentifier())
                                                      .at(Instant.now())
                                                      .build())
                                              .build()))
                                  .join();
                          if (!sendResult.isSuccess())
                            return Result.internalServerError(
                                "Demo.GeneralError",
                                "Failed calling message service: SendMessage");

                          // Response
                          return Result.ok(created);
                        })))
        .build()
        .join();


// The endpoint of sendToAccountService.
var response = accountServiceSession.acceptGatewayRequest(requestJson);
```
{% endtab %}

{% tab title="TypeScript" %}
```typescript
// Initialize builder for forwarding and service sessions, keep them linked.
const sessionBuilder = Platform.builder()

// Prepare for outgoing message calls from the account service
const messageForwardingSessionBuilder = await sessionBuilder
  // This uuid is the service id of your message service.
  .forwardingSessionBuilder("60888f37-1665-416e-a70f-09332a24f7bd")
  .withInterceptors((i) =>
    i.interceptPattern(
      UniscaleDemoMessages.Patterns.pattern,
      async (input, ctx) => {
        const requestJson = GatewayRequest.from(input, ctx).toJson()
        // This call should end up in AcceptGatewayRequest of the message
        // session that we create in a later sample.
        const response = await sendToMessageService(requestJson);
        return response
      },
    ),
  )
  .build()

// Handle incoming calls for the account service
const accountServiceSession = await sessionBuilder
  .withInterceptors((i) =>
    i.interceptRequest(
      GetOrRegister.allFeatureUsages,
      GetOrRegister.handleAsync(async (input, ctx) => {
        // For demo, we'll create a sample user as variable.
        const created = {
          handle: input,
          userIdentifier: generateUUID(),
        } as UserFull

        // Request message service to celebrate new user.
        const message = `we registered ${created.handle}`
        const dispatcher =
          await messageForwardingSessionBuilder.forTransaction(
            ctx.transactionId,
          )
        const sendResult = await dispatcher.request(
          WelcomeUser.with({
            // For demo the created user is the message sender.
            welcomedUser: {
              by: created.userIdentifier,
              at: new Date(),
            } as UserTag,
            message: message,
          } as WelcomeUserInput),
        )
        if (!sendResult.isSuccess())
          return Result.internalServerError(
            "Demo.GeneralError",
            "Failed calling message service: SendMessage",
          ) as Result<unknown> as Result<UserFull>

        // Response
        return Result<UserFull>.ok(created)
      }),
    ),
  )
  .build()
  

// The endpoint of sendToAccountService.
const response = accountServiceSession.acceptGatewayRequest(requestJson);
```
{% endtab %}
{% endtabs %}



And then the only thing left is the message service. We create a `messageServiceSession`. This service only needs to implement its features and then accept incoming requests.

{% tabs %}
{% tab title="C# .NET" %}
{% code fullWidth="true" %}
```csharp
// Create a simple message service session that we can call later in a sample
var messageServiceSession = await Platform.Builder()
    .WithInterceptors(i => i
        .InterceptMessage(
            WelcomeUser.AllFeatureUsages,
            WelcomeUser.Handle((input, ctx) =>
            {
                // Send the message into console as a test.
                Console.WriteLine($"Message: {input.Message}; " +
                                  $"By: {input.WelcomedUser.By}");
            })
        ))
    .Build();
    
    
// The endpoint of SendToMessageService.
var response = messageServiceSession.AcceptGatewayRequest(requestJson);
```
{% endcode %}
{% endtab %}

{% tab title="Python" %}
```python
# Create a simple message service session that we can call later in a sample
def handle_welcome_user(
    cinput: WelcomeUserInput, ctx: FeatureContext
) -> Result:
    print(f"Message: {cinput.message}; By: {cinput.welcomed_user.by}")
    return Result.ok(None)

message_service_session = await (
    Platform.builder()
    .with_interceptors(
        lambda i: i.intercept_request(
            WelcomeUser.all_feature_usages,
            WelcomeUser.handle(handle_welcome_user),
        )
    )
    .build()
)


# The endpoint of SendToMessageService.
response = await message_service_session.accept_gateway_request(
    request_json
)
```
{% endtab %}

{% tab title="Java" %}
```java
// Create a simple message service session that we can call later in a sample
var messageServiceSession =
    Platform.builder()
        .withInterceptors(
            i ->
                i.interceptMessage(
                    WelcomeUser.allFeatureUsages,
                    WelcomeUser.handleDirect(
                        (input, ctx) -> {
                          // Send the message into console as a test.
                          System.out.printf(
                              "Message: %s; By: %s.%n",
                              input.getMessage(),
                              input.getWelcomedUser().getBy());
                        })))
        .build()
        .join();


// The endpoint of sendToMessageService.
var response = messageServiceSession.acceptGatewayRequest(requestJson);
```
{% endtab %}

{% tab title="TypeScript" %}
```typescript
// Create a simple message service session that we can call later in a sample
const messageServiceSession = await Platform.builder()
  .withInterceptors((i) =>
    i.interceptMessage(
      WelcomeUser.allFeatureUsages,
      WelcomeUser.handleDirect((input, ctx) => {
        // Send the message into console as a test.
        console.log(
          `Message: ${input.message} By: ${input.welcomedUser?.by}`,
        )
      }),
    ),
  )
  .build()


// The endpoint of sendToMessageService.
const response = messageServiceSession.acceptGatewayRequest(requestJson);
```
{% endtab %}
{% endtabs %}



### Full working sample

Below is everything put together in a working sample with imports. In this sample, the HTTP calls have been simplified to direct references into the created sessions.

{% tabs %}
{% tab title="C# .NET" %}
{% code fullWidth="true" %}
```csharp
using Uniscale.Core;
using Uniscale.Designtime;
using UniscaleDemo.Account_1_0.Functionality.ServiceToModule.
    Account.Registration.ContinueToApplication;
using UniscaleDemo.Account.Account;
using UniscaleDemo.Messages_1_0.Functionality.ServiceToService.
    Messages.NotificationFunctionality.WelcomeMessage;
using UniscaleDemo.Messages.Messages;

// Create a simple message service session that we can call later in a sample
var messageServiceSession = await Platform.Builder()
    .WithInterceptors(i => i
        .InterceptMessage(
            WelcomeUser.AllFeatureUsages,
            WelcomeUser.Handle((input, ctx) =>
            {
                // Send the message into console as a test.
                Console.WriteLine($"Message: {input.Message}; " +
                                  $"By: {input.WelcomedUser.By}");
            })
        ))
    .Build();


// Initialize builder for forwarding and service sessions, keep them linked.
var sessionBuilder = Platform.Builder();

// Prepare for outgoing message calls from the account service
var messageForwardingSessionBuilder = await sessionBuilder
    .ForwardingSessionBuilder(
        // This Guid is the service id of your message service.
        Guid.Parse("60888f37-1665-416e-a70f-09332a24f7bd"))
    .WithInterceptors(i => i
        .InterceptPattern(UniscaleDemo.Messages.Patterns.Pattern,
            async (input, ctx) =>
            {
                var requestJson = GatewayRequest.From(input, ctx).ToJson();
                // This could just as easily be an HTTP call
                var response = await messageServiceSession
                    .AcceptGatewayRequest(requestJson);
                return response;
            }))
    .Build();

// Handle incoming calls for the account service
var accountServiceSession = await sessionBuilder
    .WithInterceptors(i => i
        .InterceptRequest(
            GetOrRegister.AllFeatureUsages,
            GetOrRegister.Handle(async (input, ctx) =>
                {
                    // For demo, we'll create a sample user as variable.
                    var created = new UserFull
                    {
                        Handle = input,
                        UserIdentifier = Guid.NewGuid()
                    };

                    // Request message service to celebrate new user.
                    var message = $"we registered {created.Handle}";
                    var dispatcher = await messageForwardingSessionBuilder
                        .ForTransaction(ctx.TransactionId);
                    var sendResult = await dispatcher.Request(
                        WelcomeUser.With(new WelcomeUserInput
                        {
                            // For demo the created user is the message sender.
                            WelcomedUser = new UserTag {
                                By = created.UserIdentifier, 
                                At = DateTime.Now
                            },
                            Message = message
                        }));
                    if (!sendResult.Success)
                        return Result<UserFull>.InternalServerError(
                            "Demo.GeneralError",
                            $"Failed calling message service: WelcomeUser");

                    // Success response
                    return Result<UserFull>.Ok(created);
                }
            )))
    .Build();


// And finally we can define the client
var clientSession = await Platform.Builder()
    .WithInterceptors(i => i
        .InterceptPattern(UniscaleDemo.Account.Patterns.Pattern,
            async (input, ctx) =>
            {
                var requestJson = GatewayRequest.From(input, ctx).ToJson();
                // This could just as easily be an HTTP call
                var response = await accountServiceSession
                    .AcceptGatewayRequest(requestJson);
                return response;
            }))
    .Build();

var dispatcher = clientSession.AsSolution(
    // This Guid is the id of your solution.
    Guid.Parse("ac43912b-50cf-439a-9652-b378b197d80a"));

// And for sample we make the call to create a new user
var createdUser = await dispatcher.Request(
    GetOrRegister.With("AwesomeUserHandle"));
Console.WriteLine(createdUser.Success
    ? $"We created user with id: {createdUser.Value.UserIdentifier}"
    : createdUser.Error.ToLongString());import uuid
```
{% endcode %}
{% endtab %}

{% tab title="Python" %}
```python
from datetime import datetime
from uniscale.core import Result, GatewayRequest
from uniscale.core.platform.platform import Platform
from uniscale.core.utilisation.utilisation_session_base import FeatureContext
from uniscale.uniscaledemo.account.patterns import Patterns as AccountPatterns
from uniscale.uniscaledemo.messages.patterns import Patterns as MessagePatterns
from uniscale.uniscaledemo.account.account.user_full import UserFull
from uniscale.uniscaledemo.messages.messages.user_tag import UserTag
from uniscale.uniscaledemo.messages_1_0.functionality.servicetoservice.messages.notificationfunctionality.welcomemessage.welcome_user import (
    WelcomeUser,
    WelcomeUserInput,
)
from uniscale.uniscaledemo.account_1_0.functionality.servicetomodule.account.registration.continuetoapplication.get_or_register import (
    GetOrRegister,
)


# Create a simple message service session that we can call later in a sample
def handle_welcome_user(
    cinput: WelcomeUserInput, ctx: FeatureContext
) -> Result:
    print(f"Message: {cinput.message}; By: {cinput.welcomed_user.by}")
    return Result.ok(None)

message_service_session = await (
    Platform.builder()
    .with_interceptors(
        lambda i: i.intercept_request(
            WelcomeUser.all_feature_usages,
            WelcomeUser.handle(handle_welcome_user),
        )
    )
    .build()
)

# Initialize builder for forwarding and service sessions, keep them linked.
session_builder = Platform.builder()

async def message_handler(cinput, ctx) -> Result:
    request_json = GatewayRequest.from_(cinput, ctx).to_json()
    # This could just as easily be an HTTP call
    response = await message_service_session.accept_gateway_request(
        request_json
    )
    return response

# Prepare for outgoing message calls from the account service
message_forwarding_session_builder = (
    await session_builder.forwarding_session_builder(
        # This uuid is the service id of your message service.
        uuid.UUID("60888f37-1665-416e-a70f-09332a24f7bd")
    )
    .with_interceptors(
        lambda i: i.intercept_pattern(MessagePatterns.pattern, message_handler)
    )
    .build()
)

async def handle_get_or_register(cinput: str, ctx: FeatureContext) -> Result:
    # For demo, we'll create a sample user as a variable.
    created = UserFull(handle=cinput, user_identifier=uuid.uuid4())

    # Request message service to celebrate new user.
    message = f"we registered {created.handle}"
    dispatcher = await message_forwarding_session_builder.for_transaction(
        ctx.transaction_id
    )

    send_result = await dispatcher.request(
        WelcomeUser.with_(
            WelcomeUserInput(
                message=message,
                welcomed_user=UserTag(
                    by=created.user_identifier, at=datetime.now()
                ),
            )
        )
    )
    if not send_result.is_success():
        return Result.internal_server_error(
            "Demo.GeneralError", "Failed calling message service: SendMessage"
        )
    # Success response
    return Result.ok(created)

# Handle incoming calls for the account service
account_service_session = await session_builder.with_interceptors(
    lambda i: i.intercept_request(
        GetOrRegister.all_feature_usages,
        GetOrRegister.handle_async(handle_get_or_register),
    )
).build()

async def account_handler(cinput, ctx) -> Result:
    request_json = GatewayRequest.from_(cinput, ctx).to_json()
    # This could just as easily be an HTTP call
    response = await account_service_session.accept_gateway_request(
        request_json
    )
    return response

# And finally we can define the client
client_session = (
    await Platform.builder()
    .with_interceptors(
        lambda i: i.intercept_pattern(AccountPatterns.pattern, account_handler)
    )
    .build()
)

dispatcher = client_session.as_solution(
    # This uuid is the id of your solution.
    uuid.UUID("ac43912b-50cf-439a-9652-b378b197d80a")
)

# And for sample we make the call to create a new user
created_user = await dispatcher.request(
    GetOrRegister.with_("AwesomeUserHandle")
)
if created_user.is_success():
    print(f"We created user with id: {created_user.value.user_identifier}")
else:
    print(created_user.error.to_long_string())
```
{% endtab %}

{% tab title="Java" %}
```java
import com.uniscale.sdk.Platform;
import com.uniscale.sdk.core.GatewayRequest;
import com.uniscale.sdk.core.Result;
import java.time.Instant;
import java.util.UUID;
import uniscaledemo.account.account.UserFull;
import uniscaledemo.account_1_0.functionality.servicetomodule.
    account.registration.continuetoapplication.GetOrRegister;
import uniscaledemo.messages.messages.UserTag;
import uniscaledemo.messages.messages.WelcomeUserInput;
import uniscaledemo.messages_1_0.functionality.servicetoservice.
    messages.notificationfunctionality.welcomemessage.WelcomeUser;


// Create a simple message service session that we can call later in a sample
var messageServiceSession =
    Platform.builder()
        .withInterceptors(
            i ->
                i.interceptMessage(
                    WelcomeUser.allFeatureUsages,
                    WelcomeUser.handleDirect(
                        (input, ctx) -> {
                          // Send the message into console as a test.
                          System.out.printf(
                              "Message: %s; By: %s.%n",
                              input.getMessage(),
                              input.getWelcomedUser().getBy());
                        })))
        .build()
        .join();

// Initialize builder for forwarding and service sessions, keep them linked.
var sessionBuilder = Platform.builder();

// Prepare for outgoing message calls from the account service
var messageForwardingSessionBuilder =
    sessionBuilder
        .forwardingSessionBuilder(
            // This uuid is the service id of your message service.
            UUID.fromString("60888f37-1665-416e-a70f-09332a24f7bd"))
        .withInterceptors(
            i ->
                i.interceptPattern(
                    uniscaledemo.messages.Patterns.pattern,
                    (input, ctx) -> {
                      var requestJson = GatewayRequest.from(input, ctx)
                          .toJson();
                      // This could just as easily be an HTTP call
                      return messageServiceSession
                          .acceptGatewayRequest(requestJson);
                    }))
        .build()
        .join();

// Handle incoming calls for the account service
var accountServiceSession =
    sessionBuilder
        .withInterceptors(
            i ->
                i.interceptRequest(
                    GetOrRegister.allFeatureUsages,
                    GetOrRegister.handle(
                        (input, ctx) -> {
                          // For demo, we'll create a sample user as a variable.
                          var created =
                              UserFull.builder()
                                  .handle(input)
                                  .userIdentifier(UUID.randomUUID())
                                  .build();

                          // Request message service to celebrate new user.
                          var message = String.format("we registered %s.%n", 
                              created.getHandle());
                          var dispatcher =
                              messageForwardingSessionBuilder
                                  .forTransaction(ctx.getTransactionId())
                                  .join();
                          var sendResult =
                              dispatcher
                                  .request(
                                      // For demo the created user is sender.
                                      WelcomeUser.with(
                                          WelcomeUserInput.builder()
                                              .message(message)
                                              .welcomedUser(
                                                  UserTag.builder()
                                                      .by(created
                                                          .getUserIdentifier())
                                                      .at(Instant.now())
                                                      .build())
                                              .build()))
                                  .join();
                          if (!sendResult.isSuccess())
                            return Result.internalServerError(
                                "Demo.GeneralError",
                                "Failed calling message service: SendMessage");

                          // Response
                          return Result.ok(created);
                        })))
        .build()
        .join();

// And finally we can define the client
var clientSession =
    Platform.builder()
        .withInterceptors(
            i ->
                i.interceptPattern(
                    uniscaledemo.account.Patterns.pattern,
                    (input, ctx) -> {
                      var requestJson = GatewayRequest.from(input, ctx)
                          .toJson();
                      // This could just as easily be an HTTP call
                      return accountServiceSession
                          .acceptGatewayRequest(requestJson);
                    }))
        .build()
        .join();

var dispatcher =
    clientSession.asSolution(
        // This uuid is the id of your solution.
        UUID.fromString("ac43912b-50cf-439a-9652-b378b197d80a"));

// And for sample we make the call to create a new user
var createdUser = dispatcher
    .request(GetOrRegister.with("AwesomeUserHandle"))
    .join();

if (createdUser.isSuccess())
  System.out.printf(
      "We created user with id: %s.%n",
      createdUser.getValue().getUserIdentifier());
else
  System.out.println(createdUser.getError().toLongString());
```
{% endtab %}

{% tab title="TypeScript" %}
```typescript
import {
  GatewayRequest,
  Platform,
  Result,
  UniscaleDemoAccount,
  UniscaleDemoMessages,
} from "@uniscale-sdk/ActorCharacter-Messagethreads"
import { generateUUID } from "@uniscale-sdk/ActorCharacter-Messagethreads/models/uuid"
import { UserFull } from "@uniscale-sdk/ActorCharacter-Messagethreads/sdk/UniscaleDemo/Account/Account"
import { GetOrRegister } from "@uniscale-sdk/ActorCharacter-Messagethreads/sdk/UniscaleDemo/Account_1_0/Functionality/ServiceToModule/Account/Registration/ContinueToApplication"
import {
  UserTag,
  WelcomeUserInput,
} from "@uniscale-sdk/ActorCharacter-Messagethreads/sdk/UniscaleDemo/Messages/Messages"
import { WelcomeUser } from "@uniscale-sdk/ActorCharacter-Messagethreads/sdk/UniscaleDemo/Messages_1_0/Functionality/ServiceToService/Messages/NotificationFunctionality/WelcomeMessage"


// Create a simple message service session that we can call later in a sample
const messageServiceSession = await Platform.builder()
  .withInterceptors((i) =>
    i.interceptMessage(
      WelcomeUser.allFeatureUsages,
      WelcomeUser.handleDirect((input, ctx) => {
        // Send the message into console as a test.
        console.log(
          `Message: ${input.message} By: ${input.welcomedUser?.by}`,
        )
      }),
    ),
  )
  .build()

// Initialize builder for forwarding and service sessions, keep them linked.
const sessionBuilder = Platform.builder()

// Prepare for outgoing message calls from the account service
const messageForwardingSessionBuilder = await sessionBuilder
  // This uuid is the service id of your message service.
  .forwardingSessionBuilder("60888f37-1665-416e-a70f-09332a24f7bd")
  .withInterceptors((i) =>
    i.interceptPattern(
      UniscaleDemoMessages.Patterns.pattern,
      async (input, ctx) => {
        const requestJson = GatewayRequest.from(input, ctx).toJson()
        // This could just as easily be an HTTP call
        const response = await messageServiceSession.acceptGatewayRequest(
          requestJson,
        )
        return response
      },
    ),
  )
  .build()

// Handle incoming calls for the account service
const accountServiceSession = await sessionBuilder
  .withInterceptors((i) =>
    i.interceptRequest(
      GetOrRegister.allFeatureUsages,
      GetOrRegister.handleAsync(async (input, ctx) => {
        // For demo, we'll create a sample user as a variable.
        const created = {
          handle: input,
          userIdentifier: generateUUID(),
        } as UserFull

        // Request message service to celebrate new user.
        const message = `we registered ${created.handle}`
        const dispatcher =
          await messageForwardingSessionBuilder.forTransaction(
            ctx.transactionId,
          )
        const sendResult = await dispatcher.request(
          WelcomeUser.with({
            // For demo the created user is the message sender.
            welcomedUser: {
              by: created.userIdentifier,
              at: new Date(),
            } as UserTag,
            message: message,
          } as WelcomeUserInput),
        )
        if (!sendResult.isSuccess())
          return Result.internalServerError(
            "Demo.GeneralError",
            "Failed calling message service: SendMessage",
          ) as Result<unknown> as Result<UserFull>

        // Response
        return Result<UserFull>.ok(created)
      }),
    ),
  )
  .build()

// And finally we can define the client
const clientSession = await Platform.builder()
  .withInterceptors((i) =>
    i.interceptPattern(
      UniscaleDemoAccount.Patterns.pattern,
      async (input, ctx) => {
        const requestJson = GatewayRequest.from(input, ctx).toJson()
        // This could just as easily be an HTTP call
        const response = await accountServiceSession.acceptGatewayRequest(
          requestJson,
        )
        return response
      },
    ),
  )
  .build()

const dispatcher = clientSession.asSolution(
  // This uuid is the id of your solution.
  "ac43912b-50cf-439a-9652-b378b197d80a",
)

// And for sample we make the call to create a new user
const createdUser = await dispatcher.request(
  GetOrRegister.with("AwesomeUserHandle"),
)
if (createdUser.isSuccess())
  console.log(
    `We created user with id: ${createdUser.value?.userIdentifier}`,
  )
else console.log(createdUser.error?.toLongString())
```
{% endtab %}
{% endtabs %}
