# IDE plugins

The idea of the plugins (Uniscale Develop) is to streamline mundane coding tasks when you start using your SDK so you can focus on implementing the actual business logic behind the endpoints. The plugin understands different parts of your services and you can just choose which part you want to start implementing and it generates a boilerplate to get you started right away.

Uniscale Develop is vendor-neutral and can seamlessly integrate with relevant code editors. Supported languages are TypeScript, Java, C#, and Python.



### Features <a href="#features" id="features"></a>

Uniscale Develop provides several code-generation commands based on the service or solution you have modeled in Uniscale. You can see all available generation commands in the "commands" section.

See all the available features for the IDE of your choice in the respective subpage:

[visual-studio-code.md](visual-studio-code.md "mention")

[visual-studio.md](visual-studio.md "mention")



### Requirements <a href="#requirements" id="requirements"></a>

To use Uniscale Develop, you must first log in to Uniscale. The workspace must be the same workspace where the used SDK was generated from i.e. your user must be in the same workspace where your modeling and SDK is.

You must have one or more Uniscale SDKs installed as a dependency. If there is only one, then that is used by default. If there are two or more, you will have to select between the available SDKs which one to use for snippet generation.&#x20;



### Commands

`Initialize - Module session`

This command generates a dispatcher through a platform session and defines a placeholder for your interceptor implementations (see Intercept commands). A helper text is printed as a comment in your code, guiding you on how to call an endpoint using the dispatcher. The command automatically uses the correct solution ID based on the SDK you are working with in the IDE.

`Initialize - Service session`

This command provides you with a standard session for handling incoming requests and also a forwarding session with a usage example. A forwarding session can be used to forward requests to other services. The command automatically uses the correct solution ID based on the SDK you are working with in the IDE.

`Intercept - Handlers with specification`

This command allows you to print both the skeleton definition of the endpoints to handle and the specification on how to implement them.

You can search through a list of available domains, service flows, and namespaces to generate all interceptors under a namespace, all interceptors within a service flow, or the interceptor for an endpoint.

`Intercept - Service Pattern`

This command allows you to add an interceptor for a selected pattern. It prepares an interceptor that passes the input and `ctx` into a gateway request, which is then converted into a JSON string. It also provides guidance on how to pass this JSON into another Uniscale session or send it over any transport protocol, and how to deserialize the response back into a `Result` object.

You can choose from a list of available patterns (Service, Namespace, Technical use case, Technical use case flow, and standalone use case flow) to add an interceptor for.

`Intercept - Service Pattern over HTTP`

This command provides the same functionality as the service pattern command, but also includes the code for making an outgoing HTTP request in the recommended way.

`Snippet - Incoming gateway request handle`

This command is designed to initialize the transport endpoint on a hosted service receiving an incoming gateway request. It guides the user on how to use the Uniscale session to pass the raw JSON string into it and ensure the response uses the `ToJson` method for correct serialization.

`Snippet - Terminology validation (Module)`\
This command is designed to assist the user in validating a terminology code. It provides a selection of available terminologies within the SDK, and upon selection, it prints a snippet that uses the dispatcher and the generated pattern for that terminology to trigger the validation method. It also provides guidance on handling the response if the validation fails.

`Snippet - Terminology validation (Service)`

Same as terminology validation for module but it prints a snippet that uses the forwarding session and the context's transaction id to acquire a forwarding dispatcher. It then uses this dispatcher and the generated pattern for the selected terminology to trigger the validation method. It also provides guidance on handling the response if the validation fails and suggests returning the response directly as this code will normally be generated within an interceptor.

`Snippet - Outgoing service to service request`

This command is designed to assist the user in making a service call from one service to another. It prompts the user to select am endpoint, uses the forwarding session and the context's transaction id to acquire a forwarding dispatcher, and prints a request to the selected endpoint. It also handles required character arguments and failed responses.

`Specification - Endpoint Specification`

This command is designed to print the specification for an endpoint directly. It is useful when you already have the interceptor set up and just want to print the specification into it. It can also assist in re-printing the specification into an interceptor if the requirements have changed due to a new service revision.

`Specification - Endpoint Specification (RAW)`

This command is designed to print the specification for an endpoint directly. It is particularly useful when the user is not using the Uniscale session and wants the specification printed directly into, for instance, an HTTP route handler. It can also assist in re-printing the specification if the requirements have changed due to a new service revision.

`Specification - Use case implementation`

This command is designed to provide AI-generated hints using the specification, allowing the user to explain in plain text how they want the code to behave when calling the endpoints. The command also generates the specification in a way that even the non-endpoint related parts of the specification can be taken into account when the AI writes the code. These include functional acceptance criteria regarding pure frontend related concepts.

The user can search through a list of functional and technical use cases that they want to print the specification hints for.

`Specification - Use case implementation (RAW)`

Same as regular use case implementation but it prints the output without any hints to how to use the Uniscale SDK. This is useful when the user does not intend to use the Uniscale session in their implementation.



