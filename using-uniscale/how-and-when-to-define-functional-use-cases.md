---
description: >-
  Functional use cases are used to specify the user interaction within your
  module. Let's look at how to use them to lock down the requirements right
  away.
---

# How and when to define functional use cases

Structure vs behaviour

As explained in the previous guide Pages and sections are used to represent the structure and high level description of your specification. The Functional use cases are there for you to define the high level and in detail end user behaviour in your system. This is where you can go into detail on expected details down to contents of dropdowns, what happens when the user clicks a button or describing even cross page behaviour.

<figure><img src="../.gitbook/assets/image (8).png" alt=""><figcaption><p>Define Functional use cases within the module, Pages or Sections to describe user interaction. This is also the link into services.</p></figcaption></figure>

It is also helpful to look at Functional use cases as a level of detail. When someone reads the specification without showing Functional use cases they should be left with a high level overview of the solution for any stakeholder to align on. When then displaying the Functional use cases without UX flows and Designer notes the reader should be left with a high level over view of the solutions end user behaviour for stakeholders to align on. When displaying UX flows and designer notes the reader should be left with an in detail understanding of how the functionality should behave when the user interacts with it. Even one level deeper is to display the Service flows which describes the technical flow needed to implement the described functionality.



## What does a Functional use case consist of?

At the top level a functional use case consists of a description where you can describe the high level functionality provided towards the end user. The intentions for defining it may be that you need to explain a flow that the user can go through like searching for something. It could also be that you need to describe some data being loaded into the user interface or some UI design guidelines for a user interface.

{% hint style="info" %}
Functional use cases are split into UX product notes and UI designer notes to separate the graphical element specification from the user interaction. They can both be specified in details using UX flows and designer notes.
{% endhint %}



### UX product notes and UX flows

The UX product notes is where you can go into more detail regarding the user experience part of the use case if required. This can also be left blank if you have no additional information to add. Under the UX product notes you can also add one or more UX flows. These are used both to describe details of the flow with acceptance criteria's and the link into Service flows.



### UI designer notes and designer notes

It is important to distinguish user experience from user design as it is not necessarily the same person accountable for it. As such we have split UI designer notes out so that UI design specification can be handled separately. As with UX product notes it consist of a general description which can be utilized if needed and a list of designer notes describing the different points to communicate regarding the design.



## Defining Functional use cases

As with all other parts of the specification you can use the / command and the ... menu of elements to create new Functional use cases. They can be placed directly on the module, under a page or a section. This allows you to place them structurally where they belong.&#x20;

For instance the ones placed on the level of a module or a page might define a high level flow of a user navigating through pages / sections of the module. Further down in sections you might place Functional use cases describing exactly how buttons, dropdowns, collapsible areas or any other element behaves. This allows you to drill down to the necessary details you want to express.



***

## Summary

Functional use cases allow you to express the end user behaviour using multiple levels of granularity. As opposed to the pages and sections they express behaviour rather than structure. Within Functional use cases you can define UX product notes with their flows and UI designer not with their detailed notes. This allows you to break the specification down to it's necessary detail.
