---
description: >-
  Let's look at how to nail the structure of your solution specification. Learn
  how to break functionality down into modules. Learn about module, services and
  their impact on scaling your organization.
---

# Get started with a solution

## Conceptual introduction

Learn how a solution is broken down into each element. You can watch the video or read the explanation below:

{% embed url="https://www.youtube.com/watch?index=1&list=PL5utFq0uexyEWGiAWXFbh1ncy2rbimVGi&v=SHpHH7qhk3Q" %}
Video: Uniscale Describe: Solution Design Flow \[3:31]
{% endembed %}



### What does a solution consist of?

A solution consists of modules and services:

* **Solution:** The overall product or project that you are working on.
* **Modules:** It is the grouping of the end user functionality in your solution that belongs together and changes together. We will dive into modules further in this article: [get-started-with-a-module.md](get-started-with-a-module.md "mention")
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



### How to define module and service boundaries

The key to succeeding with your Uniscale solution design is the way you split the solution functionality into modules and services.&#x20;

<details>

<summary>The challenge explained</summary>

When attempting to scale a software product organization, it becomes challenging when multiple teams attempt to deliver functionality into the same modules and services. This leads to parallel deliveries from multiple teams to the same functionality, resulting in high organizational friction due to conflicts and misalignments in functionality.

</details>

#### The boundary of a module or a service is defined by:

* Functionality that belongs together and frequently changes together.
* Is owned by a single team or department in your organization.&#x20;

When the functionality of your solution is divided into modules, the majority of your functionalities should pertain to only a single module. Additionally, the services should use the same structure and follow the team or department that owns that module.

<figure><img src="../../.gitbook/assets/slide - 36 - new.png" alt=""><figcaption><p>Modules and services should be owned by a single entity in your organization. This will provide you with good coherent specifications and effective deliveries.</p></figcaption></figure>



***

## Guide: Create and describe your solution

### Step 1: Create your solution

<figure><img src="../../.gitbook/assets/CleanShot 2024-03-15 at 11.04.58.gif" alt=""><figcaption><p>Guide how to create a solution</p></figcaption></figure>

<details>

<summary>Step-by-step guide to create a solution</summary>

**Step 1: Go to Solutions**

From your workspace: **Go to "Solutions".**

<img src="../../.gitbook/assets/CleanShot 2024-03-15 at 11.12.02.png" alt="Go to the solution table from the workspace dashboard " data-size="original">

**Step 2: Click "Create solution"**

And click the **"Create solution"** button in the top right corner.

<img src="../../.gitbook/assets/CleanShot 2024-03-18 at 13.38.11@2x.png" alt="Click &#x22;Create solution&#x22;" data-size="original">

**Step 3: Fill out the solution details**

When you create a solution, you give it a name, owner, and description and then click "**Submit**".

1. **Name**: The name of your solution, it can be a code name or product name.
2. **Owner:** The person responsible for decisions related to the solution.
3. **Description:** A short description, or elevator pitch for the problem your solution addresses.

<img src="../../.gitbook/assets/CleanShot 2024-03-15 at 11.19.00.png" alt="Fill out your solution details " data-size="original">

</details>



### Step 2: Describe your solution

Start by providing a high-level description of your solution. This will help set the scene for you and others.&#x20;

{% hint style="info" %}
Type "/" or use the "..." to trigger the command menu. \
The command menu contains all the options within the element you are located in.&#x20;
{% endhint %}

<figure><img src="../../.gitbook/assets/CleanShot 2024-03-26 at 11.09.55.png" alt=""><figcaption><p>Using command menu to create a new element</p></figcaption></figure>

<details>

<summary>Using generative AI to write</summary>

If your plan includes the generative AI functionality you can get started by getting some ideas from the AI. This is helpful for instance when wanting to get help on making your specification well articulated and readable.&#x20;

Remember that even though the AI can help you express things more clearly you are the one responsible for making sure that your intentions and requirements are communicated.&#x20;

</details>



### Step 3: Create your first module

Now that you have created your solution, you can break it down into modules. To do so, please go to the following page: [get-started-with-a-module.md](get-started-with-a-module.md "mention")



***

## Summary

Solutions consist of modules and services where modules describe end-user functionality and services describe the technical requirements needed to deliver that functionality. It is crucial to put thought into how you split a solution into modules and services. It relates to the ownership within your organization and the ability of your organization to scale with your product.
