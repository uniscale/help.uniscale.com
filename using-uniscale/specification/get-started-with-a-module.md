---
description: >-
  How to structure a module specification and separate high level descriptions
  from detailed functionality specifications. Allow all stakeholders to
  communicate over the same specification.
---

# How to get started with a module

## What are the building blocks of a module?

Modules are structured using Pages, Sections, and Functional use cases.&#x20;

### Pages and Sections&#x20;

These are the elements that you will use to align the structure of your application in the same way as the product. In that way, it will be easier to navigate your way within a module in relation to your product.

<figure><img src="../../.gitbook/assets/slide - 37 - new.png" alt=""><figcaption><p>The structural breakdown of a module specification using Pages and sections.</p></figcaption></figure>



### Functional use cases

Functional use cases are used to define the user behavior within the module. Each functional use case consists of a description, where you can describe the high-level user behavior.&#x20;

#### UX flows

UX flows (user experience flows) are used to further break down your Functional use case. In this way, the reader can choose to read the specification through the preferred level of detail. Even designer notes have a section within Functional use cases to explain details around look and feel.

<figure><img src="../../.gitbook/assets/Concept - new.png" alt=""><figcaption><p>Define Functional use cases within the module, Pages or Sections to describe user interaction. This is also the link into services.</p></figcaption></figure>

The connection between the service documentation and the module specification happens through the UX flows in Functional use cases. Through them, you can link to service flows which is a service's way of expressing intent of usage to some of its endpoints.

{% hint style="info" %}
As the specification will evolve, it is helpful to be thoughtful of the structure. It should be easy to focus only on parts of the specification while having all the contextual information available.
{% endhint %}



## Cater to your audience

As these are the functional requirements for your solution, it is important that all your stakeholders can easily navigate and make sense of your specifications. This ensures optimal communication and alignment. To achieve this you must define the right information within the right elements.&#x20;

{% hint style="info" %}
Use Pages and Sections for high-level explanations while using Functional use cases for more detailed explanations. In this way, when filtering out Functional use cases, you have a high-level point of view for aligning all stakeholders.
{% endhint %}

Within Pages and Sections, you can describe high-level specifications of your functionality. In this way, all stakeholders can use this part of the specification to make sure that everyone has a high-level alignment of the functionality and the intentions that led to its current state. From there the reader can enable Functional use cases or even UX flows and designer notes to dig into the details needed to implement the requirements.



## Make use of visuals

{% hint style="info" %}
Type "/" or click the "..." menu to start creating content within your specification.
{% endhint %}

To start your module specification, we recommend using mocks of the user interface. You can insert images of your mock, screenshot, or even drawing right into your module specification.

This helps the reader better have the context and understand what you are trying to achieve with your solution.&#x20;



## Specify the first module revision

Let's dive in and specify the first revision of a module. We will go through the elements used to write it and some decisions behind why and how.

{% embed url="https://www.youtube.com/watch?list=PL5utFq0uexyEWGiAWXFbh1ncy2rbimVGi&v=VZkJOCtMGfI" %}
Let's go through and write our first module revision specification
{% endembed %}



***

## Summary

Modules consist of Pages and sections to define the overall and structural build-up. They are used to communicate high-level functionality for all stakeholders. The details about the user interaction are described in Functional use cases. Read more about those in the next article.
