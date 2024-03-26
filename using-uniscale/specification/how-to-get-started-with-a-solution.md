---
description: >-
  Lets look at how to nail the structure of your solution specification. Learn
  how to break functionality down into modules. Learn about module, services and
  their impact on scaling your organization.
---

# How to get started with a solution

## Conceptual introduction

Learn how a solution is broken down into each element.



### What does a solution consist of?

A solution consists of modules and services:

* **Solution:** The overall product or project that you are working on.
* **Modules:** It is the grouping of the end user functionality in your solution that belongs together and changes together. We will dive into modules further in this article: [how-to-get-started-with-a-module.md](how-to-get-started-with-a-module.md "mention")
* **Services:** Describe the requirements for the underlying technical flows that will enable you to build this functionality.

<figure><img src="../../.gitbook/assets/Concept - new.png" alt=""><figcaption><p>Solution components </p></figcaption></figure>



### Continuous development

You will incrementally write parts of your specifications as you deliver functionality through projects or sprints. In Uniscale, this is achieved by making revisions to your modules and services to plan each project or sprint and ensure a smooth transition into the code phase.

{% hint style="info" %}
Learn more about about revisions here: [module-revisions-readying-and-approving.md](module-revisions-readying-and-approving.md "mention")
{% endhint %}

<figure><img src="../../.gitbook/assets/CleanShot 2024-03-26 at 10.45.02.png" alt=""><figcaption><p>Uniscale in the DevOps process</p></figcaption></figure>



### Uniscale as the single source of truth

Over time, your solution specification will follow your product as the single source of truth for all intentions and decisions that went into making your product what it is today. This is key to being able to make good decisions in the future.

<figure><img src="../../.gitbook/assets/slide - 06.png" alt=""><figcaption><p>Uniscale Design's relation to a product roadmap. Single source of truth through many iterations over time.</p></figcaption></figure>



## How to define module and service boundaries

The key to succeeding with your Uniscale solution design is the way you split the solution functionality into modules and services.&#x20;

<details>

<summary>The challenge explained</summary>

When attempting to scale a software product organization, it becomes challenging when multiple teams attempt to deliver functionality into the same modules and services. This leads to parallel deliveries from multiple teams to the same functionality, resulting in high organizational friction due to conflicts and misalignments in functionality.

</details>

#### The boundary of a module or a service is defined by:

* Functionality that belongs together and frequently changes together.
* Is owned by a single team or department in your organization.&#x20;

When the functionality of your solution is divided into modules, the majority of your functionalities should pertain to only a single module. Additionally, the services should follow the same structure and follow the team or department that owns that module.

<figure><img src="../../.gitbook/assets/slide - 36 - new.png" alt=""><figcaption><p>Modules and services should be owned by a single entity in your organization. This will provide you with good coherent specifications and effective deliveries.</p></figcaption></figure>



***

## Guide: Create and describe the first solution and module

If you haven't already, start by creating a solution [guide-create-solution.md](guide-create-solution.md "mention").

Now, let's dive into producing some valuable content. You will have the same rich text capabilities wherever you are within the Uniscale specification and documentation.

{% hint style="info" %}
Type "/" or use the "..." to trigger the command menu. \
The command menu contains all the options within the element you are located in.&#x20;
{% endhint %}

<figure><img src="../../.gitbook/assets/CleanShot 2024-03-26 at 11.09.55.png" alt=""><figcaption><p>Using command menu to create a new element</p></figcaption></figure>

### Step 1: Describe your solution

Start by providing a high-level description of your solution. This will help set the scene for you and others.

<details>

<summary>Using generative AI to write</summary>

If your plan includes the generative AI functionality you can get started by getting some ideas from the AI. This is helpful for instance when wanting to get help on making your specification well articulated and readable.&#x20;

Remember that even though the AI can help you express things more clearly you are the one responsible for making sure that your intentions and requirements are communicated.&#x20;

</details>



### Step 2: Create your first module

To create a module, you can either use the "/" menu or you can use the "Create module" button in the top solution context bar.

<figure><img src="../../.gitbook/assets/image (2) - new - new.png" alt=""><figcaption><p>Create modules either through the / command or by using the solution context menu at the top.</p></figcaption></figure>

{% hint style="info" %}
By selecting a module in the solution context dropdown, you can get to the module focus view. In there, you can approve your module revision, look at previous revisions, and more.
{% endhint %}



### Step 3: Specifying your first module revision

Let's dive in and specify the first revision of a module. We will go through the elements used to write it and some decisions behind why and how.

{% embed url="https://www.youtube.com/watch?list=PL5utFq0uexyEWGiAWXFbh1ncy2rbimVGi&v=VZkJOCtMGfI" %}
Let's go through and write our first module revision specification
{% endembed %}



***

## Summary

Solutions consist of modules and services where modules describe end-user functionality and services describe the technical requirements needed to deliver that functionality. It is crucial to put thought into how you split a solution into modules and services. It relates to the ownership within your organization and the ability of your organization to scale with your product.\
You can create new modules by either using the "/" command or creating one from the solution context menu at the top of the page.
