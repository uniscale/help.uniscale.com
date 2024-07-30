---
description: >-
  Learn how to describe your detailed specification along with the best
  practices to follow. This includes breaking down the structure of your
  solution and involving a UI/UX designer.
---

# Detailed specification

Before you begin to describe your detailed specification, please make sure to have completed the high-level specification: [high-level-specification](high-level-specification/ "mention")

## Introduction

At this stage, your idea is ready to make the transition from "abstract" to "concrete" and this is where you will involve a Product Designer (eg. UX or UI designer) who will start to break down the specification and design the product. This includes:

* The best approach to solving the described problem: Should it be an app, website, software, a combination, or perhaps just a paper?
* Describing the intended user experience.
* How should the user interface look and feel?



## Describe the detailed specification

{% hint style="info" %}
To begin describing the detailed specification, we recommend familiarizing yourself with the elements in a solution. These are all explained here: [solution-basics](solution-basics/ "mention")
{% endhint %}

{% embed url="https://www.youtube.com/watch?v=m2ZrQtW60Vc" %}
Video: Tutorial: Detailed specification
{% endembed %}

{% hint style="info" %}
**Create visuals for your modules**

If you haven't already, a good place to start is by inserting images with mockups or wireframes of your solution. Adding visuals will help get a clear overview of what needs to be broken down.
{% endhint %}



### Break down the structure of your solution

With your visuals created, you will begin to form the layout and interface of your solution.&#x20;

To break down your solution, make use of [#pages](solution-basics/#pages "mention") and [#sections](solution-basics/#sections "mention"). This will represent the structure of your solution.

For each element created, add a short description and an image to highlight that specific part of the solution.

See an example of a Page:

<figure><img src="../../.gitbook/assets/CleanShot 2024-07-03 at 08.50.09@2x.png" alt=""><figcaption><p>Template - "Messages Wall" Page</p></figcaption></figure>

And one for a Section:

<figure><img src="../../.gitbook/assets/CleanShot 2024-07-03 at 08.51.11@2x.png" alt=""><figcaption><p>Template - "New posts" section</p></figcaption></figure>



### Describe the user behavior with Functional use cases

With your structure defined, it is time to describe the behavior of your solution.

{% hint style="info" %}
In the high-level specification, the purpose of the Functional use case is to describe the high-level user behavior **abstractly**. Now, you will begin to describe the **concrete** use cases for each page and section.&#x20;
{% endhint %}

#### Create a Functional use cases.

A Functional use case represents the user beahvior within a module and page.

<figure><img src="../../.gitbook/assets/CleanShot 2024-07-02 at 14.25.33@2x.png" alt=""><figcaption><p>Create a functional use case</p></figcaption></figure>

#### Describe your Functional use case.&#x20;

This description should include a detailed explanation of a specific interaction between a user and an application to achieve a particular goal.&#x20;

It outlines the steps involved, the actors, the conditions under which the interaction occurs, and the expected outcomes.&#x20;

<figure><img src="../../.gitbook/assets/CleanShot 2024-07-02 at 14.28.46@2x.png" alt=""><figcaption><p>Describe your functional use case</p></figcaption></figure>

#### Add UI Designer notes.&#x20;

Your UI Designer notes should include the detailed annotations and explanations provided by a UI  designer to convey design decisions, guidelines, and specific instructions for implementing a user interface.

<figure><img src="../../.gitbook/assets/CleanShot 2024-07-02 at 14.32.46@2x.png" alt=""><figcaption><p>UI Designer notes</p></figcaption></figure>

#### Add UX Product notes with UX flows

The UX Product notes allow you to add notes and provide a detailed description regarding the intended user experience for a specific functional use case.

On the other hand, the UX flows describe the detailed behaviors within functional use cases.

<figure><img src="../../.gitbook/assets/CleanShot 2024-07-02 at 14.33.42@2x.png" alt=""><figcaption><p>UX Product notes</p></figcaption></figure>

#### Enrich UX flows with Functional acceptance criteria.

Your acceptance criteria will be a list of qualifications that the implementation of the UX flow needs to fulfil.

<figure><img src="../../.gitbook/assets/CleanShot 2024-07-02 at 14.35.53@2x.png" alt=""><figcaption><p>Functional acceptance criteria</p></figcaption></figure>

UX flows are the lowest level of detail in your functional specification. When these are ready, your specification is ready.

***



## Next steps

* Approve your first revision: [module-revision.md](module-revision.md "mention")
* Generate the SDK: [sdk-basics](../implementation/sdk-basics/ "mention")
* Proceed to [service-linking](../documentation/service-linking/ "mention")
