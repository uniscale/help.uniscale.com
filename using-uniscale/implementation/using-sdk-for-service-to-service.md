---
description: Learn how to use the SDK for a service to service.
---

# Using SDK for service to service

Real-world applications often need to call another service from the initial one that is called. We have created `ForwardingSession` to make service-to-service calls. Forwarding session-related tools help you with handling context and transaction errors.&#x20;

{% hint style="warning" %}
It is important that you use the `ForwardingSession` for service-to-service calls to properly connect your services and the requests sent between those.
{% endhint %}

Below is a sample where we have `clientSession` that is used to create a request into account service (represented by `accountServiceSession`) which in turn makes service-to-service calls into message service (represented by `messageServiceSession`).&#x20;



## Creating a sample in stages

Let's go through the flow, starting from the `clientSession`. We want to register a new user with the handle "AwesomeUserHandle". First, we create a pattern interceptor that sends a request to our account service, initializes the dispatcher, and makes a request.

{% tabs %}
{% tab title="C# .NET" %}
{% code title="Original client" fullWidth="true" %}
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
{% code title="Original client" %}
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
{% endcode %}
{% endtab %}

{% tab title="Java" %}
{% code title="Original client" %}
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
{% endcode %}
{% endtab %}

{% tab title="TypeScript" %}
{% code title="Original client" %}
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
{% endcode %}
{% endtab %}

{% tab title="PHP" %}
{% code title="Original client" %}
```php
<?php

require 'vendor/autoload.php';

use Uniscale\Uniscaledemo\Account\Functionality\ServiceToModule\Account\Registration\GetOrRegister;
use Ramsey\Uuid\Uuid;
use Uniscale\Http\Result;
use Uniscale\Models\BackendActions\GatewayRequest;
use Uniscale\Platform\Platform;
use Uniscale\Uniscaledemo\Account\Patterns as AccountPatterns;


// Create the client session with pattern interceptor
$clientSession = Platform::builder()
    ->withInterceptors(function ($interceptor) {
        $interceptor->interceptPattern(
            AccountPatterns::$pattern,
            function ($input, $ctx) {
                $requestJson = GatewayRequest::from($input, $ctx)->toJson();
                // This call should end up in acceptGatewayRequest of the account
                // session that we create in a later sample.
                $response = sendToAccountService($requestJson);
                return $response;
            }
        );
    })
    ->build();

$dispatcher = $clientSession->asSolution(Uuid::fromString('ac43912b-50cf-439a-9652-b378b197d80a'));

// Make the call to create a new user
$createdUser = $dispatcher->request(
    GetOrRegister::with("AwesomeUserHandle")
);

if ($createdUser->isSuccess()) {
    echo "We created user with id: " . $createdUser->getValue()->userIdentifier;
} else {
    echo $createdUser->getError()->toLongString();
}
```
{% endcode %}
{% endtab %}
{% endtabs %}



Account service receives the original client's request. We know that our account service will need to be forwarding the call on top of receiving it, so we will need separate sessions for each. The builder for the session which is forwarding calls to a message service (`messageForwardingSession`) is created separately and can be reused if needed. Then in `accountServiceSession` we create the user, create a dispatcher based on `messageForwardingSession` and make a request from account service to message service.&#x20;

{% tabs %}
{% tab title="C# .NET" %}
{% code title="Account service" fullWidth="true" %}
```csharp
// Initialize builder for forwarding and service sessions, keep them linked.
var sessionBuilder = Platform.Builder();

// Prepare for outgoing message calls from the account service
var messageForwardingSession = await sessionBuilder
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
                    var dispatcher = await messageForwardingSession
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

                    // Success response
                    return Result<UserFull>.Ok(created);
                }
            )))
    .Build();


// The HTTP endpoint of account service.
var response = accountServiceSession.AcceptGatewayRequest(requestJson);
```
{% endcode %}
{% endtab %}

{% tab title="Python" %}
{% code title="Account service" %}
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
message_forwarding_session = (
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
    dispatcher = await message_forwarding_session.for_transaction(
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


# The HTTP endpoint of account service.
response = await account_service_session.accept_gateway_request(
    request_json
)
```
{% endcode %}
{% endtab %}

{% tab title="Java" %}
{% code title="Account service" %}
```java
// Initialize builder for forwarding and service sessions, keep them linked.
var sessionBuilder = Platform.builder();

// Prepare for outgoing message calls from the account service
var messageForwardingSession =
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
                              messageForwardingSession
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

                          // Success response
                          return Result.ok(created);
                        })))
        .build()
        .join();


// The HTTP endpoint of account service.
var response = accountServiceSession.acceptGatewayRequest(requestJson);
```
{% endcode %}
{% endtab %}

{% tab title="TypeScript" %}
{% code title="Account service" %}
```typescript
// Initialize builder for forwarding and service sessions, keep them linked.
const sessionBuilder = Platform.builder()

// Prepare for outgoing message calls from the account service
const messageForwardingSession = await sessionBuilder
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
        const dispatcher = await messageForwardingSession.forTransaction(
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

        // Success response
        return Result<UserFull>.ok(created)
      }),
    ),
  )
  .build()


// The HTTP endpoint of account service.
const response = accountServiceSession.acceptGatewayRequest(requestJson);
```
{% endcode %}
{% endtab %}

{% tab title="PHP" %}
{% code title="Account service" %}
```php
<?php

use Uniscale\Uniscaledemo\Account\Functionality\ServiceToModule\Account\Registration\GetOrRegister;
use Ramsey\Uuid\Uuid;
use Uniscale\Http\Result;
use Uniscale\Models\BackendActions\GatewayRequest;
use Uniscale\Platform\Platform;
use Uniscale\Uniscaledemo\Messages\Messages\UserTag;
use Uniscale\Uniscaledemo\Messages\Messages\WelcomeUserInput;
use Uniscale\UniscaleDemo\Messages\Patterns as MessagePatterns;
use Uniscale\Uniscaledemo\Messages_1_0\Functionality\Servicetoservice\Messages\Notificationfunctionality\Welcomemessage\WelcomeUser;

require 'vendor/autoload.php';

// Initialize builder for forwarding and service sessions, keep them linked.
$sessionBuilder = Platform::builder();

// Prepare for outgoing message calls from the account service
$messageForwardingSession = $sessionBuilder
    ->forwardingSessionBuilder(
    // This Guid is the service id of your message service.
        Uuid::fromString('60888f37-1665-416e-a70f-09332a24f7bd'))
    ->withInterceptors(function ($interceptor) {
        $interceptor->interceptPattern(
            MessagePatterns::$pattern,
            function ($input, $ctx) {
                $requestJson = GatewayRequest::from($input, $ctx)->toJson();
                // This call should end up in AcceptGatewayRequest of the message
                // session that we create in a later sample.
                $response = sendToMessageService($requestJson);
                return $response;
            }
        );
    })
    ->build();

// Handle incoming calls for the account service
$accountServiceSession = $sessionBuilder
    ->withInterceptors(function ($interceptor) use ($messageForwardingSession) {
        $interceptor->interceptRequest(
            GetOrRegister::ALL_FEATURE_USAGES,
            GetOrRegister::handle(function ($input, $ctx) use ($messageForwardingSession) {
                // For demo, we'll create a sample user as variable.
                $created = (object)[
                    'handle' => $input,
                    'userIdentifier' => Uuid::uuid4(),
                ];

                // Request message service to celebrate new user.
                $message = "we registered {$created->handle}";
                $dispatcher = $messageForwardingSession->forTransaction($ctx->transactionId);

                $sendResult = $dispatcher->request(
                    WelcomeUser::with(WelcomeUserInput::fromObject(
                        (object)['welcomedUser' => UserTag::fromObject(
                            (object)[
                                'by' => $created->userIdentifier,
                                'at' => new DateTime(),
                            ]),
                            'message' => $message]))
                );

                if (!$sendResult->isSuccess()) {
                    return Result::internalServerError(
                        "Demo.GeneralError",
                        "Failed calling message service: SendMessage"
                    );
                }

                // Success response
                return Result::ok($created);
            })
        );
    })
    ->build();

// The HTTP endpoint of account service.
$response = $accountServiceSession->acceptGatewayRequest($requestJson);
```
{% endcode %}
{% endtab %}
{% endtabs %}



And then the only thing left is the message service. We create a `messageServiceSession`. This service only needs to implement its features and then accept incoming requests.

{% tabs %}
{% tab title="C# .NET" %}
{% code title="Message service" fullWidth="true" %}
```csharp
// Create a simple message service session that we can call later in a sample
var messageServiceSession = await Platform.Builder()
    .WithInterceptors(i => i
        .InterceptMessage(
            WelcomeUser.AllFeatureUsages,
            WelcomeUser.Handle((input, ctx) =>
            {
                if (string.IsNullOrEmpty(input.Message))
                {
                    return Result.BadRequest(
                        ErrorCodes.Messages.ValidationError);
                }
                // Send the message into console as a test.
                Console.WriteLine($"Message: {input.Message}; " +
                                  $"By: {input.WelcomedUser.By}");
                return Result.Ok();
            })
        ))
    .Build();


// The HTTP endpoint of message service.
var response = messageServiceSession.AcceptGatewayRequest(requestJson);
```
{% endcode %}
{% endtab %}

{% tab title="Python" %}
{% code title="Message service" %}
```python
# Create a simple message service session that we can call later in a sample
def handle_welcome_user(
    cinput: WelcomeUserInput, ctx: FeatureContext
) -> Result:
    if not cinput.message:
        return Result.bad_request(ErrorCodes.messages.validation_error)
    
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


# The HTTP endpoint of message service.
response = await message_service_session.accept_gateway_request(
    request_json
)
```
{% endcode %}
{% endtab %}

{% tab title="Java" %}
{% code title="Message service" %}
```java
// Create a simple message service session that we can call later in a sample
var messageServiceSession =
    Platform.builder()
        .withInterceptors(
            i ->
                i.interceptMessage(
                    WelcomeUser.allFeatureUsages,
                    WelcomeUser.handle(
                        (input, ctx) -> {
                          if (StringUtils.isEmpty(input.getMessage()))
                          {
                            return Result.badRequest(
                                ErrorCodes.messages.validationError);
                          }
                          // Send the message into console as a test.
                          System.out.printf(
                              "Message: %s; By: %s.%n",
                              input.getMessage(), 
                              input.getWelcomedUser().getBy());
                          return Result.ok();
                        })))
        .build()
        .join();


// The HTTP endpoint of message service.
var response = messageServiceSession.acceptGatewayRequest(requestJson);
```
{% endcode %}
{% endtab %}

{% tab title="TypeScript" %}
{% code title="Message service" %}
```typescript
// Create a simple message service session that we can call later in a sample
const messageServiceSession = await Platform.builder()
  .withInterceptors((i) =>
    i.interceptMessage(
      WelcomeUser.allFeatureUsages,
      WelcomeUser.handle((input, ctx) => {
        if (!input.message)
          return Result.badRequest(ErrorCodes.messages.validationError)
        
        // Send the message into console as a test.
        console.log(
          `Message: ${input.message} By: ${input.welcomedUser?.by}`,
        )
        return Result.ok(undefined)
      }),
    ),
  )
  .build()


// The HTTP endpoint of message service.
const response = messageServiceSession.acceptGatewayRequest(requestJson);
```
{% endcode %}
{% endtab %}

{% tab title="PHP" %}
{% code title="Message service" %}
```php
<?php

use Uniscale\Http\Result;
use Uniscale\Platform\Platform;
use Uniscale\Uniscaledemo\Messages_1_0\ErrorCodes;
use Uniscale\Uniscaledemo\Messages_1_0\Functionality\Servicetoservice\Messages\Notificationfunctionality\Welcomemessage\WelcomeUser;

// Create a simple message service session that we can call later in a sample
$messageServiceSession = Platform::builder()
    ->withInterceptors(function ($interceptor) {
        $interceptor->interceptMessage(
            WelcomeUser::ALL_FEATURE_USAGES,
            WelcomeUser::handle(function ($input, $ctx) {
                if (empty($input->message)) {
                    return Result::badRequest(ErrorCodes::$messages->validationError);
                }

                // Send the message into console as a test.
                error_log("Message: {$input->message} By: {$input->welcomedUser->by}");
                return Result::ok();
            })
        );
    })
    ->build();

// The HTTP endpoint of message service.
$response = $messageServiceSession->acceptGatewayRequest($requestJson);
```
{% endcode %}
{% endtab %}
{% endtabs %}



## Error handling

Forwarding sessions have built-in support for gathering errors from all levels of the service-to-service flow. In other words, errors from outgoing calls are automatically added to the handler's response. In the sample we've created above, if we were to send an empty message into the message service, the original caller would receive an Error that would look similar to this in JSON:

{% code title="Sample error as JSON" %}
```json
{
  "code": "Demo.GeneralError",
  "details": {
    "integrationCode": null,
    "requestedFeature": "UniscaleDemo.Account_1_0.Functionality.ServiceToModule.Account.Registration.ContinueToApplication.GetOrRegister",
    "technicalError": "Failed calling message service: WelcomeUser",
    "userError": null
  },
  "related": [],
  "parent": {
    "code": "Platform.Fundamentals.SDK.ClientIOError",
    "details": {
      "integrationCode": null,
      "requestedFeature": null,
      "technicalError": "Errors collected from forwarding related requests",
      "userError": null
    },
    "related": [
      {
        "code": "UniscaleDemo.Messages.Messages.ValidationError",
        "details": {
          "integrationCode": "60888f37-1665-416e-a70f-09332a24f7bd",
          "requestedFeature": "UniscaleDemo.Messages_1_0.Functionality.ServiceToService.Messages.NotificationFunctionality.WelcomeMessage.WelcomeUser",
          "technicalError": "",
          "userError": "The specified input is not valid. Please contact support."
        },
        "related": [],
        "parent": null
      }
    ],
    "parent": null
  }
}
```
{% endcode %}

So the errors from deeper into the service-to-service call will be stored inside the parent's related errors for each level.



## Fully working single file sample

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
                if (string.IsNullOrEmpty(input.Message))
                {
                    return Result.BadRequest(
                        ErrorCodes.Messages.ValidationError);
                }
                // Send the message into console as a test.
                Console.WriteLine($"Message: {input.Message}; " +
                                  $"By: {input.WelcomedUser.By}");
                return Result.Ok();
            })
        ))
    .Build();


// Initialize builder for forwarding and service sessions, keep them linked.
var sessionBuilder = Platform.Builder();

// Prepare for outgoing message calls from the account service
var messageForwardingSession = await sessionBuilder
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
                    var dispatcher = await messageForwardingSession
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
    : createdUser.Error.ToLongString());
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
    if not cinput.message:
        return Result.bad_request(ErrorCodes.messages.validation_error)
    
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
message_forwarding_session = (
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
    dispatcher = await message_forwarding_session.for_transaction(
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
                    WelcomeUser.handle(
                        (input, ctx) -> {
                          if (StringUtils.isEmpty(input.getMessage()))
                          {
                            return Result.badRequest(
                                ErrorCodes.messages.validationError);
                          }
                          // Send the message into console as a test.
                          System.out.printf(
                              "Message: %s; By: %s.%n",
                              input.getMessage(), 
                              input.getWelcomedUser().getBy());
                          return Result.ok();
                        })))
        .build()
        .join();

// Initialize builder for forwarding and service sessions, keep them linked.
var sessionBuilder = Platform.builder();

// Prepare for outgoing message calls from the account service
var messageForwardingSession =
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
                              messageForwardingSession
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
      WelcomeUser.handle((input, ctx) => {
        if (!input.message)
          return Result.badRequest(ErrorCodes.messages.validationError)
        
        // Send the message into console as a test.
        console.log(
          `Message: ${input.message} By: ${input.welcomedUser?.by}`,
        )
        return Result.ok(undefined)
      }),
    ),
  )
  .build()

// Initialize builder for forwarding and service sessions, keep them linked.
const sessionBuilder = Platform.builder()

// Prepare for outgoing message calls from the account service
const messageForwardingSession = await sessionBuilder
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
        const dispatcher = await messageForwardingSession.forTransaction(
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

{% tab title="PHP" %}
```php
<?php

use Uniscale\Platform\Platform;
use Uniscale\Result\Result;
use Uniscale\UniscaleDemo\Account\Account;
use Uniscale\UniscaleDemo\Account\Registration\GetOrRegister;
use Uniscale\UniscaleDemo\Account\Patterns as AccountPatterns;
use Uniscale\UniscaleDemo\Messages\WelcomeUser;
use Uniscale\UniscaleDemo\Messages\WelcomeUserInput;
use Uniscale\UniscaleDemo\Messages\UserTag;
use Uniscale\UniscaleDemo\Messages\Patterns as MessagePatterns;
use Uniscale\GatewayRequest;

require 'vendor/autoload.php';

class SessionManager {
    public static $messageServiceSession;
    public static $messageForwardingSession;
    public static $accountServiceSession;
    public static $clientSession;

    public static function initializeSessions() {
        // Create a simple message service session that we can call later in a sample
        self::$messageServiceSession = Platform::builder()
            ->withInterceptors(function ($interceptor) {
                $interceptor->interceptMessage(
                    WelcomeUser::allFeatureUsages(),
                    WelcomeUser::handle(function ($input, $ctx) {
                        if (empty($input->message)) {
                            return Result::badRequest(ErrorCodes::messages()->validationError());
                        }

                        // Send the message into console as a test.
                        error_log("Message: {$input->message} By: {$input->welcomedUser->by}");
                        return Result::ok(null);
                    })
                );
            })
            ->build();

        // Initialize builder for forwarding and service sessions, keep them linked.
        $sessionBuilder = Platform::builder();

        // Prepare for outgoing message calls from the account service
        self::$messageForwardingSession = $sessionBuilder
            // This uuid is the service id of your message service.
            ->forwardingSessionBuilder("60888f37-1665-416e-a70f-09332a24f7bd")
            ->withInterceptors(function ($interceptor) {
                $interceptor->interceptPattern(
                    MessagePatterns::pattern(),
                    function ($input, $ctx) {
                        $requestJson = GatewayRequest::from($input, $ctx)->toJson();
                        // This could just as easily be an HTTP call
                        $response = self::$messageServiceSession->acceptGatewayRequest($requestJson);
                        return $response;
                    }
                );
            })
            ->build();

        // Handle incoming calls for the account service
        self::$accountServiceSession = $sessionBuilder
            ->withInterceptors(function ($interceptor) {
                $interceptor->interceptRequest(
                    GetOrRegister::allFeatureUsages(),
                    GetOrRegister::handleAsync(function ($input, $ctx) {
                        // For demo, we'll create a sample user as a variable.
                        $created = (object) [
                            'handle' => $input,
                            'userIdentifier' => self::generateUUID(),
                        ];

                        // Request message service to celebrate new user.
                        $message = "we registered {$created->handle}";
                        $dispatcher = self::$messageForwardingSession->forTransaction($ctx->transactionId);
                        $sendResult = $dispatcher->request(
                            WelcomeUser::with((object) [
                                'welcomedUser' => (object) [
                                    'by' => $created->userIdentifier,
                                    'at' => new DateTime(),
                                ],
                                'message' => $message,
                            ])
                        );

                        if (!$sendResult->isSuccess()) {
                            return Result::internalServerError(
                                "Demo.GeneralError",
                                "Failed calling message service: SendMessage"
                            );
                        }

                        // Response
                        return Result::ok($created);
                    })
                );
            })
            ->build();

        // And finally we can define the client
        self::$clientSession = Platform::builder()
            ->withInterceptors(function ($interceptor) {
                $interceptor->interceptPattern(
                    AccountPatterns::pattern(),
                    function ($input, $ctx) {
                        $requestJson = GatewayRequest::from($input, $ctx)->toJson();
                        // This could just as easily be an HTTP call
                        $response = self::$accountServiceSession->acceptGatewayRequest($requestJson);
                        return $response;
                    }
                );
            })
            ->build();
    }

    private static function generateUUID() {
        // Generate a UUID
        return bin2hex(random_bytes(16));
    }
}

// Initialize the sessions
SessionManager::initializeSessions();

$dispatcher = SessionManager::$clientSession->asSolution(
    // This uuid is the id of your solution.
    "ac43912b-50cf-439a-9652-b378b197d80a"
);

// And for sample we make the call to create a new user
$createdUser = $dispatcher->request(
    GetOrRegister::with("AwesomeUserHandle")
);

if ($createdUser->isSuccess()) {
    error_log("We created user with id: {$createdUser->value->userIdentifier}");
} else {
    error_log($createdUser->error->toLongString());
}
```
{% endtab %}
{% endtabs %}

