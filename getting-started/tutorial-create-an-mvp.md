---
description: >-
  Learn how to use Uniscale from end to end by creating a sample project. This
  will function as a minimum viable product.
---

# Tutorial: Create an MVP

## Introduction

The purpose of this article is to create a minimum viable product called "UserSolution" in Uniscale. You can follow along and replicate the steps in your Uniscale workspace.

What you will learn:

1. [specification](../using-uniscale/specification/ "mention"): Write the product specification.
2. [documentation](../using-uniscale/documentation/ "mention"): Create and model the service needed.
3. [implementation](../using-uniscale/implementation/ "mention"): Generate the Uniscale SDK and implement it into your IDE.



## Create a sample project

### Functional Specification

Here we will describe the functional requirements.

1. Create a `solution` called "UserSolution"
   1. Idea: Use the solution description template here [template-solution-description.md](../using-uniscale/specification/high-level-specification/template-solution-description.md "mention") and use the generative AI in Uniscale to prefill the text.
2. Create a `module` called: "UserModule"
3. Create a `page` called "User Listing Page"
4. Create a `Functional use case` called: "User Listing Table"
   1. Include a description: "Be able to list all users in the solution"
   2. Add a `UX flow` called "Should have name, email, phone, and gender"
   3. Add a `Service flow` called: "UserService"

<figure><img src="../.gitbook/assets/CleanShot 2024-07-23 at 11.13.15.gif" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
We have described our solution's functional requirements and are ready to move to the next phase.
{% endhint %}



### Service linking

First, we will link the Service flow to a Service. For a detailed walkthrough, please check: [#tutorial-service-linking](../using-uniscale/documentation/service-linking/#tutorial-service-linking "mention")

<figure><img src="../.gitbook/assets/CleanShot 2024-07-23 at 11.17.12.gif" alt=""><figcaption></figcaption></figure>

1. Go to the module "UserModule"
2. Navigate to "Service linking"
3. Click "Add service draft"
   1. Name: "UserService"
   2. Click "Create root namespace"
4. In Overview, expand the "User Listing Table" to find the Service flow called "UserService_"_
5. Drag the Service flow to the Service "UserService"
6. Create the service by selecting "Create service"



### Service modeling

Here we will describe the technical documentation to support the functional requirements.

{% embed url="https://www.youtube.com/watch?v=ITWeHW91fnY" %}

1. Click on "Go to" to enter the service editor
2. Add an [`aggregate`](#user-content-fn-1)[^1] named "User"
3. Add the [`properties`](#user-content-fn-2)[^2] and define them with the details below:

<table><thead><tr><th width="159">Property name</th><th width="152">Property type</th><th width="223">Data type</th><th>Additional settings</th></tr></thead><tbody><tr><td>Email</td><td>Native type</td><td>String</td><td><ul><li><a data-footnote-ref href="#user-content-fn-3">Validation</a></li><li><a data-footnote-ref href="#user-content-fn-4">Sample</a></li></ul></td></tr><tr><td>Gender</td><td>Native type</td><td>Terminology</td><td><ul><li><a data-footnote-ref href="#user-content-fn-5">Terminologies</a></li></ul></td></tr><tr><td>Name</td><td>Native type</td><td>String</td><td><ul><li><a data-footnote-ref href="#user-content-fn-6">Sample</a></li></ul></td></tr><tr><td>Phone</td><td>Value object</td><td>New - Product owned</td><td><ul><li><a data-footnote-ref href="#user-content-fn-7">Value object type</a></li><li><a data-footnote-ref href="#user-content-fn-8">Add properties</a></li></ul></td></tr></tbody></table>

4. Complete the `aggregate` and `value object`.
5. Create the [`endpoint`](#user-content-fn-9)[^9]&#x20;
   1. Select "Link endpoint" from the menu
   2. Endpoint origin: "Create new endpoint"
   3. Endpoint type "Request/respond"
   4. Endpoint behavior: "Get"
   5. Endpoint action: "Users"
   6. Select "Create endpoint"
   7. Add endpoint input
      1. Create a `value object`
         1. Name "Empty"
         2. Property type: Value object - Structure
         3. Mark as complete
         4. Data representation: Select the value object "Empty"
         5. Cardinality: "Single"
   8. Add endpoint output
      1. Data representation: Select the aggregates "Value objects" and "UserIdentifier"
         1. Cardinality: "Multiple"
   9. Mark the endpoint as complete



### Service locking and approving

You will lock and approve each service revision as you want to keep track of your changes over time.

* Select "Ready all"
* In the overview, select "Set all to ready"
* Select "Approve"
  * Name it "Initial revision"
  * Select "Submit"&#x20;

{% hint style="success" %}
We have completed the technical documentation and are ready to begin the implementation.
{% endhint %}



## SDK generation

Now we will generate the SDK and begin the technical implementation. For a detailed walkthrough, please check [#generating-the-sdk](../using-uniscale/implementation/introduction-to-sdk/#generating-the-sdk "mention")

1. Go to the SDK Portal
2. Libraries setup:
   1. Select service the service you want to generate the SDK for
   2. Select your preferred programming languages.
3. Click "Save changes"

<figure><img src="../.gitbook/assets/CleanShot 2024-07-24 at 11.39.29@2x.png" alt=""><figcaption></figcaption></figure>



### Use the Uniscale SDK

With the sample project described in Uniscale, it is time to begin the technical implementation.&#x20;

* Learn how to utilize the Uniscale SDK: [library-implementation-basics](../using-uniscale/implementation/library-implementation-basics/ "mention")
* Integrate Uniscale with your IDE: [ide-plugins](../using-uniscale/implementation/ide-plugins/ "mention")
* Find the relevant article based on your intention: [implementation](../using-uniscale/implementation/ "mention")

{% hint style="success" %}
Congratulations! We have now fully implemented the solution "UserSolution".&#x20;
{% endhint %}



## Build your solution

You are now ready to build your solution in Uniscale:

* Visit: [quick-start-guide.md](quick-start-guide.md "mention")
* Need help? Book a meeting and let us help you: [https://www.uniscale.com/onboarding](https://www.uniscale.com/onboarding)

[^1]: Aggregates represent the main data containers for your properties and data modeling.\
    Learn more: [#aggregates](../using-uniscale/documentation/service-basics/#aggregates "mention")

[^2]: A property represents a data field that holds values defining characteristics of an object or entity within Uniscale\
    Learn more: [#properties](../using-uniscale/documentation/service-modeling/properties-and-terminologies.md#properties "mention")

[^3]: * Field restriction: Forced validation
    * Name: "Valid Email"
    * Validation type: string -> REGEX
    * Expression: ^\[\w-.]+@(\[\w-]+.)+\[\w-]{2,4}$
    * Description: "Should be a valid email"

[^4]: * "test@example.com"

[^5]: * "Male"
    * "Female"

[^6]: * "John Doe"

[^7]: "Structure"

[^8]: * CountryCode
    * Number

[^9]: In Uniscale, we follow the same understanding and concept around endpoints as the industry.

    \
    Learn more: [#endpoints](../using-uniscale/documentation/service-basics/#endpoints "mention")
