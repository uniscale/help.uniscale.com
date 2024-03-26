---
description: >-
  Functional use cases are used to specify the user interaction within your
  module. Let's look at how to use them to lock down the requirements right
  away.
---

# Functional use cases

## Structure vs behaviour

### Pages and Sections for structure

As explained in the previous guide, [get-started-with-a-module.md](get-started-with-a-module.md "mention"), Pages and Sections are used to represent the **structure** and high-level description of your specification.&#x20;

<figure><img src="../../.gitbook/assets/Frame 10314.png" alt=""><figcaption><p>The structure of a module is defined by its pages and sections</p></figcaption></figure>

### Functional use cases for behaviour

The Functional use cases enable you to define the end-user **behaviour** in your system in a detailed way. Examples of this include the contents of dropdowns, what happens when the user clicks a button, or describing even cross-page behaviour.



## What does a Functional use case consist of?

A Functional use case can be broken down into the following:

* [#description](functional-use-cases.md#description "mention")
* [#ux-product-notes-and-ux-flows](functional-use-cases.md#ux-product-notes-and-ux-flows "mention")
  * [#functional-acceptance-criteria](functional-use-cases.md#functional-acceptance-criteria "mention")
  * [#service-flows](functional-use-cases.md#service-flows "mention")
* [#ui-designer-notes-and-designer-notes](functional-use-cases.md#ui-designer-notes-and-designer-notes "mention")

### Description

A Functional use case consists of a description where you can describe the high-level functionality provided to the end user. The intention for defining it may be that you need to explain a flow that the user can go through like searching for something. It could also be that you need to describe some data being loaded into the user interface or some UI design guidelines for a user interface.



### UX product notes and UX flows

This is where you go into more detail with the user experience of the use case. This can also be left blank if you have no additional information to add.&#x20;

In addition, you can add UX flows that are used both to describe details of the flow with functional acceptance criteria and link into Service flows:

#### Functional acceptance criteria

This is what allows you to explain exactly how the UX flow should behave.&#x20;

#### Service flows

Functional use cases can be broken into UX flows that can further be linked to Service flows. This is what connects the module specification and the service documentation.

By linking a Service flow to a UX flow, you can express how a service is intended to use some of its endpoints.

<figure><img src="../../.gitbook/assets/image.avif" alt=""><figcaption><p>Define Functional use cases within the module, Pages or Sections to describe user interaction. This is also the link into services.</p></figcaption></figure>



### UI designer notes and designer notes

It is important to distinguish user experience (UX) from user interface (UI) design as it is not necessarily the same person accountable for it.&#x20;

As such we have split UI designer notes out so that UI design specifications can be handled separately. As with UX product notes it consists of a general description which can be utilized if needed and a list of designer notes describing the different points to communicate regarding the design.



***

## How to define Functional use cases

You can use the "/" command or the "..." menu to create new Functional use cases. They can be placed directly on the module, under a page or a section. This allows you to place them structurally where they belong.&#x20;

For instance, the ones placed on the level of a module or a page might define a high-level flow of a user navigating through pages/sections of the module. Further down in sections you might place Functional use cases describing exactly how buttons, dropdowns, collapsible areas or any other element behaves. This allows you to drill down to the necessary details you want to express.



***

## Summary

Functional use cases allow you to express the end user behaviour using multiple levels of granularity. As opposed to the pages and sections they express behaviour rather than structure. Within Functional use cases, you can define UX product notes with their flows and UI designer not with their detailed notes. This allows you to break the specification down to its necessary detail.
