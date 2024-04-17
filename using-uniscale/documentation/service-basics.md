# Service basics

## Overall structure

<figure><img src="../../.gitbook/assets/image (46).png" alt=""><figcaption></figcaption></figure>

## Service Composition: Understanding the Key Elements

Services are multifaceted, incorporating various elements that work cohesively to deliver functionality. This article delves into the primary components involved in service design, their application, objectives, and underlying principles. By dissecting these elements, we aim to provide a clearer understanding of what goes into creating a robust service.



```
// Example of a service with various levels of namespaces 
// and functionality
Service 
├─ Namespace
|   └─ Endpoint A
|   └─ Endpoint B
|   └─ Technical Usecase 
|      └─ Technical Usecase Flow 
└─ Empty namespace
└─ Namespace
   ├─ Aggregate A
   ├─ Aggregate B
   └─ Value object
   └─ Namespace
      └─ Property group
```

<figure><img src="../../.gitbook/assets/image (47).png" alt=""><figcaption></figcaption></figure>

## Namespaces

#### Understanding Namespaces in Your Service Architecture

Namespaces play a crucial role in the hierarchical organization of your service. Initially, they function to provide a structured framework. However, as your library evolves, namespaces become pivotal for identification purposes.

{% hint style="info" %}
Because we want to enable you to express your domain you should make sure that the hierarchy and naming of your namespace reflects the problem domain you intend to fulfil through this service.
{% endhint %}

#### Examples of namespace structure for a service:

```
Account (root level)
├─ Users
|   └─ Actions
└─ Sessions
   ├─ Activity
   └─ Backlog sessions
```

#### Revision cycle & update cycle

Namespaces are subject to the [locking/unlocking/readying](../specification/module-revision.md) process within a revision. This means that editors of a service can manage the content via each of those statuses as needed.&#x20;

The name of a namespace is strictly managed through locking and unlocking while the description are easily editable. The reason being that the namespace forms the location of endpoints and data contracts all the way into the SDK so changing a namespace name structurally changes the location of things in the SDK.

***

## Use cases

Use cases ( UC) come in two forms <mark style="color:purple;background-color:purple;">**`Functional`**</mark> and <mark style="color:purple;background-color:purple;">**`technical`**</mark>.&#x20;

Functional UCs paint a more general picture of how a user might interact with your business to reach their goals. Instead of focusing on technical detail, it’s a cause-and-effect description of different inputs.

{% hint style="info" %}
This type of UC is encountered and created from inside the [specification](../specification/solution-basics.md#functional-use-case).&#x20;
{% endhint %}

In Uniscale, the main differentiation factor for the UCs is their technical intention.

{% tabs %}
{% tab title="Functional use cases" %}
The difference is Functional use cases are defined in and owned by the Module as it is describing end user functionality. The functional use cases can be connected to either standalone or technical use case flows. However only standalone and technical use case flows defined within Service To Module.
{% endtab %}

{% tab title="Technical use cases" %}
They are use cases owned and maintained by the service itself.
{% endtab %}
{% endtabs %}

### Technical use cases&#x20;

The technical use case does not describe how the end user interacts. It rather is a group of flows that the services exposes as a larger group of functionality that belongs together. For instance a use case for a service could be mail sending management where it exposes flows for sending mail, checking status of sent mails and for instance hourly stats.

It does not describe the end user functionality, that will always be described through a module but it describes a larger set of technical functionality that the service wants to expose to it's users (developers for other services / frontends)



#### Revision cycle & update cycle

UCs are subject to the [locking/unlocking/readying](broken-reference) process within a revision. This means that editors of a service can manage the content via each of those statuses as needed.&#x20;

## Use case flows&#x20;

Different types of flows (technical / standalone) form the specification of endpoints. They represent intention of use of an endpoint and if an endpoint is not linked into at least one flow it will not become part of the SDK as it has no intention of use.

### Standalone use case flow

Use case flows represent (UCF), as the name suggests, can be used in one or more functional use cases (end user flows) if service to module. Or as a single standalone flow against another service (if service to service)

A functional UCF contains&#x20;

* a title
* a Rich Text description
* Possible functional Acceptance criteria
* and a list of linked endpoints

### Technical use case flows

They can have any technical intention, as they are a clearly defined larger use case that is owned by the service itself.

A  technical UCF contains:&#x20;

* a title
* a Rich Text description
* possible Technical Acceptance criteria
* and a list of linked endpoints

#### Revision cycle & update cycle

UCFs are subject to the [locking/unlocking/readying](broken-reference) process within a revision. This means that editors of a service can manage the content via each of those statuses as needed.&#x20;

<figure><img src="../../.gitbook/assets/image (48).png" alt=""><figcaption></figcaption></figure>

## End points

In Uniscale, we follow the same understanding and concept around endpoints as the industry.&#x20;

We must first distinguish between APIs and Endpoints as those can be quite familiar terms, with slight differences though.

### **Endpoint vs. API**

It’s important to note that **endpoints** and **APIs** are different.&#x20;

An endpoint is a component of an API, while an API is a set of rules that allow two applications to share resources. An Endpoint is the definition, structure and traits of a services exposed functionality. An API is the concrete implementation of that Endpoint determining location and means of transport. Endpoint is abstract API is concrete.

Example, an Endpoint exposed over HTTP is an HTTP API. An endpoint handled in a Uniscale Interceptor is a Uniscale API

***

As such, coming back to the definition of endpoints, they represent the **configuration of the expected behavior of the API**, together with the expected **payloads** for the possible request and response. Quite a bit to take in so let's break that down.

### **Configuration of the expected behavior of the API**

An endpoint will be defined by:

* behavior type: message or Request response
* owning namespace (location in SDK structure)
* behavior ( create, read, etc)
* name ( predefined based on behavior or custom )&#x20;
* description optional

### Payloads

Depending on the type, and endpoint can contain **one** ( Message)  or **two** payloads (Request - Response)

<figure><img src="../../.gitbook/assets/image (49).png" alt=""><figcaption></figcaption></figure>

## Error codes

Once your endpoints are configured and set up with their payloads, they can be enriched with more configuration on how they will interact with outside systems or requests.

Initially, every endpoint assumes a happy scenario where no complications or bad scenarios can occur. The reality is different of course and for various reasons, your frontend can present various scenarios where the data is wrong, or missing, or the backend cannot process the requested information.

<figure><img src="../../.gitbook/assets/image (50).png" alt=""><figcaption></figcaption></figure>

In Uniscale you can enrich each endoints with direct Error codes to cover those exact scenarios. For each error code, you can provide:

* a system code
* a user message

If you use the Uniscale session and interceptors the error response management is automatically handled through call chains. Meaning a frontend calling a service, calling another service.

<figure><img src="../../.gitbook/assets/image (51).png" alt=""><figcaption></figcaption></figure>

***

## Data contracts

Structuring your data can be done in multiple ways in Uniscale, and as such we have provided various top-level "containers" or "contracts" to manage their scope, and bounded context, in this way facilitating easier management of their Single source of truth.

#### Revision cycle & update cycle

Data contracts are subject to the [completion](broken-reference) process within a revision. This means that editors of a service can manage the content via each of those statuses as needed.&#x20;

<figure><img src="../../.gitbook/assets/image (52).png" alt=""><figcaption></figcaption></figure>

### Aggregates

Within DDD, aggregates represent the main data containers for your properties and data modeling. They are mainly characterized by a Single source of truth for individual properties and act as an umbrella for all the values within the same concept. The main definition of an Aggregate is that it is data that is referenceable by an identifier.

Aggregates are unique by identifier, which is automatically generated based on the aggregate name.  As such checking if two aggregates are equal is done by comparing their identifiers.

<figure><img src="../../.gitbook/assets/CleanShot 2024-04-16 at 17.11.16@2x.png" alt=""><figcaption></figcaption></figure>

Aggregates are placed under a namespace which acts as its owner.

**Example of aggregates:**

* User
* Person
* Order

In Uniscale, aggregates have by default an aggregate identifier created automatically which follows the aggregate name. Afterward, an aggregate can be expanded with a flat or nested structure of properties.&#x20;

<figure><img src="../../.gitbook/assets/image (54).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (55).png" alt=""><figcaption></figcaption></figure>

### Value objects&#x20;

Value objects represent data contracts that are slightly different that aggregates. They are unique by content and as such, they can be quite simple in structure or even standalone.&#x20;

Value objects are placed under a namespace which acts as its owner.

**Example of value objects:**

* Address
* SearchPayload

There are 2 types of Value objects

* type alias : A type alias is a native type with a specific meaning (ex. Gender). For instance if an endpoint wants to use a native type as it's input/output it must declare a type alias value object and use that.&#x20;
* type structure: a nested structure of properties  (ex. SearchPayload). This is encountered in situations where the request of an endpoint is a fixed structure that is always the same. But its not necessarily an aggregate.



Value objects can be referred to as other aggregates, value objects and property groups. Editing them anywhere in the interface will also update the source of truth at its origin.

<figure><img src="../../.gitbook/assets/CleanShot 2024-04-16 at 17.04.46.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (57).png" alt=""><figcaption></figcaption></figure>

### Property groups

Once further into your modelling, you will reuse certain properties from across various aggregates and value objects, also with different cardinalities in mind. Exploring such scenarios, we can have:&#x20;

Example

<figure><img src="../../.gitbook/assets/CleanShot 2024-04-16 at 17.05.00.png" alt=""><figcaption></figcaption></figure>

Property groups can be explain as a way of composing data from different value objects and aggregates to be used in Endpoint payloads. The only place and main place to use property groups is as a payload for  endpoints, being in a **Message** or a **Request-response** situation.

***

## Native type system

A **native data type** is a classification of data that tells the library generator how the library intends to use the data. In Uniscale we provide all the most commonly used data types. They are:&#x20;

<table><thead><tr><th width="164">Native type</th><th>Represents</th><th>Example</th></tr></thead><tbody><tr><td>GUID </td><td>a uniquely generated identifier</td><td>c5f364fa-1d39-4de5-abdf-c1e6a54d05a6</td></tr><tr><td>terminology</td><td>Collection of terms</td><td><p><code>{</code></p><p><code>dk :"Denmark",</code><br><code>no: "Norway",</code></p><p><code>...</code><br><code>}</code></p></td></tr><tr><td>date </td><td>Day-month-year</td><td>2022-09-27</td></tr><tr><td>datetime</td><td>Date with timestamp</td><td>2022-09-27 18:00:00.000</td></tr><tr><td>boolean </td><td>logical true or false</td><td>true, false</td></tr><tr><td>float </td><td>fractional numbers</td><td>64bit floats </td></tr><tr><td>integer </td><td>whole number</td><td>64bit integers</td></tr><tr><td>string </td><td>A sequence of characters</td><td>"hello world"</td></tr></tbody></table>

{% hint style="info" %}
Note : UTF is used as an variable-length character encoding standard.
{% endhint %}

## Technical intentions&#x20;

At its baseline, every functionality in a service should exist for a purpose and intent. That intent can be internal or external. Towards functionality (solution or module), or another system ( service or infrastructure)

<figure><img src="../../.gitbook/assets/image (59).png" alt=""><figcaption></figcaption></figure>

<mark style="color:purple;">**`Service to module`**</mark>

All the functionality a service provides means to be exposed to a Frontend, a module, or a solution.

<mark style="color:purple;">**`Service to service`**</mark>

All the functionality a service provides means to be exposed to a system, in the shape of another service can sometimes be referred to as Backend communicating with another backend.

<mark style="color:purple;">**`Service to infrastructure`**</mark>

All the functionality a service provides means to expose an infrastructure as a whole, usually Storage, Networking, or any other IaaS scenarios.

{% hint style="info" %}
Only standalone use case flows and technical use cases in a service is governed by technical intentions
{% endhint %}
