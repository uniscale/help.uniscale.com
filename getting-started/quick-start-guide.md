---
description: In this guide, we will show you the basics of getting started with Uniscale.
---

# Quick start guide

## New to Uniscale?

Get a quick introduction and watch our product video here: [#what-is-uniscale](../#what-is-uniscale "mention")



## Get started <a href="#get-started" id="get-started"></a>

{% hint style="success" %}
Before kick-starting your Uniscale journey you should:

1. [Create an account](https://help.uniscale.com/account-and-preferences/create-an-account)
2. [Create a workspace](https://help.uniscale.com/workspace-administration/manage-workspaces/create-a-workspace)
3. [Invite to a workspace](https://help.uniscale.com/workspace-administration/manage-workspaces/invite-to-a-workspace)

When this is done, you are ready to follow the guide below on how to build better software.
{% endhint %}

***



## Phase 1: Specification <a href="#design-your-solution" id="design-your-solution"></a>

{% hint style="info" %}
The specification, also known as “Functional Requirement Specification”, is a document used to describe a solution's intended capabilities, appearance, and interactions with users.&#x20;

Learn more: [specification](../using-uniscale/specification/ "mention")
{% endhint %}

<details>

<summary>To describe your specification, start by creating a solution</summary>

Within your Uniscale workspace, create a solution to describe your product and outline the functional specifications.

<img src="../.gitbook/assets/CleanShot 2024-04-11 at 15.03.56.gif" alt="Create solution" data-size="original">

</details>



### High-level specification

<details>

<summary>Intro to high-level specification</summary>

Here you will describe the overall solution. This part is done from an abstract view, meaning that it is not about solving the actual problem, but rather explaining the problem and desired outcome carefully.&#x20;

Things you may include:

* Abstract Description
* Purpose and motivation
* High-level requirements
* High-level end-user behavior

This is typically defined by the Founder, Visionary, Product Owner, or someone who understands the [solution](https://help.uniscale.com/using-uniscale/specification/solution-basics).

</details>

<details>

<summary>Describe your high-level specification</summary>

Begin with an introduction to your solution:&#x20;

1. What: A solution description including a few high-level functionalities.
2. Why: The purpose and motivation
3. Who: Who will be using your product? List the various actors.
4. High-level requirements

For a detailed overview of how to describe your specification: [tutorial-high-level-specification](../using-uniscale/specification/tutorial-high-level-specification/ "mention")

You can also use our [template-solution-description.md](../using-uniscale/specification/tutorial-high-level-specification/template-solution-description.md "mention")t to help you better structure and articulate your solution.

</details>

<details>

<summary>Define and describe your modules</summary>

1. Define and create your modules: For best practices on what modules to create, visit this article: [#module](../using-uniscale/specification/solution-basics/#module "mention")
2. Describe your modules: Write a short description and include the relevant high-level functionalities and actors related to this module. See [#create-and-describe-your-first-modules](../using-uniscale/specification/tutorial-high-level-specification/#create-and-describe-your-first-modules "mention")for more details.
3. Describe the high-level end-user behavior: This is done by creating a `Functional use case` inside your module. See [#describe-the-user-behavior-with-functional-use-cases](../using-uniscale/specification/tutorial-detailed-specification.md#describe-the-user-behavior-with-functional-use-cases "mention")for more details.
4. Enrich your `Functional use case` with `Acceptance criteria.`&#x20;

For a detailed overview of how to describe your specification: [tutorial-high-level-specification](../using-uniscale/specification/tutorial-high-level-specification/ "mention")

</details>

{% embed url="https://www.youtube.com/watch?list=PL5utFq0uexyGOAVoZxLdRIG6ti7yXqlbs&v=xtzqXVHMjpM" %}
Tutorial: High-level specification
{% endembed %}

#### **Next steps**

* Learn how to approve and lock your modules: [module-revision.md](../using-uniscale/specification/module-revision.md "mention")
* Generate the SDK: [introduction-to-sdk.md](../using-uniscale/implementation/introduction-to-sdk.md "mention")
* Continue to [#detailed-documentation](quick-start-guide.md#detailed-documentation "mention")



### Detailed specification

<details>

<summary>Introduction to detailed specification</summary>

This is where you will start to design how the actual product will look and feel. Where high-level specification is abstract, here you will define concretely how the product will work:

* Should it be an app, website, software, physical paper, or a combination?
* How should the user interface look and feel?
* The overall layout of your solution including visuals (mockups or wireframes),
* How should the product work - eg. what pages will you need, what buttons to include, what should happen when clicking on each button, and what should happen in case of errors?

For this part, you will involve a product designer (eg. UX/UI designer) who will start to break down the high-level specification and design the product.

Learn here how to invite people:[invite-to-uniscale.md](../workspace-administration/manage-workspaces/invite-to-uniscale.md "mention")

</details>

<details>

<summary>Describe your detailed specification</summary>

1. Use `Pages` and `Sections` to break down the layout and structure of your solution
2. A best practice is to include mockups or wireframes for each part of your solution
3. Include UX requirements:
   1. Break down your modules and pages into `Functional use cases.`
   2. Include relevant `UX flows`
   3. Describe your `UX flows` and include `Functional acceptance criteria`
4. Include UI requirements: Use `Designer notes` to describe the look and feel in addition to other descriptions that are helpful to the front-end developer.

Watch the video below or read more here: [tutorial-detailed-specification.md](../using-uniscale/specification/tutorial-detailed-specification.md "mention")

</details>

{% embed url="https://www.youtube.com/watch?index=2&list=PL5utFq0uexyGOAVoZxLdRIG6ti7yXqlbs&v=m2ZrQtW60Vc" %}
Tutorial: Detailed specification
{% endembed %}

#### **Next steps**

* Learn how to approve and lock your modules:[module-revision.md](../using-uniscale/specification/module-revision.md "mention")
* Generate the SDK: [introduction-to-sdk.md](../using-uniscale/implementation/introduction-to-sdk.md "mention")
* Proceed to [#phase-2-service-linking](quick-start-guide.md#phase-2-service-linking "mention")

***



## Phase 2: Service linking

{% hint style="info" %}
Service linking is where you bridge your functional specification to your technical documentation.
{% endhint %}

<details>

<summary>Introduction to service linking</summary>

Typically, a Solution Architect or Technical Lead handles this phase. They translate customer requirements into logical service boundaries by developing the services needed to meet the specified requirements.

Learn how to invite people: [invite-to-uniscale.md](../workspace-administration/manage-workspaces/invite-to-uniscale.md "mention")

</details>

<details>

<summary>Create your service linking</summary>

1. Start by going through your `UX flows` and create `Service flows`
2. Go to `Service linking` and `Add service draft +`
3. Drag and drop each service link to the service draft.

Watch the video below or read more here: [service-linking](../using-uniscale/documentation/service-linking/ "mention")

</details>

#### Next step

* Proceed to further document your services in [#phase-3-documentation](quick-start-guide.md#phase-3-documentation "mention")

***



## Phase 3: Documentation

{% hint style="info" %}
The documentation also referred to as Technical documentation, is where you define the requirements and the building blocks to support your functional specification.
{% endhint %}



### High-level documentation

<details>

<summary>Introduction to high level documentation</summary>

The documentation often referred to as "Technical Documentation," is where the focus shifts to the technical details of your product.

This part is typically created by experts such as Tech Leads or Solution Architects. They ensure the technical and non-technical aspects of your solution are aligned, even if they are not directly involved in coding.

</details>

<details>

<summary>Describing your high-level documentation</summary>

As you have now linked your `UX flows` to `Service flows`,  you will start to document the intention and purpose of each service.&#x20;

Now you can include a description of each service to document the service functionality requirements.

![](<../.gitbook/assets/CleanShot 2024-06-12 at 10.45.23@2x.png>)

See a detailed guide to describing your documentation: [service-basics.md](../using-uniscale/documentation/service-basics.md "mention")

</details>



### Detailed documentation

<details>

<summary>Introduction to detailed documentation</summary>

This is where you define all concrete actions and data contracts to fulfill all specified technical functionality.

This part includes:

* Endpoint modeling
* Error code and sample data
* Data contracts modeling
* Data validations

</details>

<details>

<summary>Describing your detailed documentation</summary>

1. Navigate to the service and begin to document the technical aspect.
2. For each service, you can enrich with:
   1. Child namespace&#x20;
   2. Endpoint
   3. Aggregate with Native type and  Sample value
   4. Value object
   5. Property group
   6. Standalone use case flow
   7. Technical use case

<img src="../.gitbook/assets/image (1) (3).png" alt="Preview of modelling view tab for the &#x22;Account&#x22; service in the Demo solution" data-size="original">

See a detailed guide to describing your documentation: [service-basics.md](../using-uniscale/documentation/service-basics.md "mention")

</details>

<details>

<summary>Service approval and revisions</summary>

Now that you have documented your services, it is time to ready and approve each one before proceeding to generate the SDK.

Learn how to do so here: [service-revisions.md](../using-uniscale/documentation/service-revisions.md "mention")

</details>

***



## Phase 4: SDK library

{% hint style="info" %}
This is the toolbox that the developers can use to build the product. The toolbox consists of all the information that is created in the specification and documentation. It contains everything that you need to do the communication between your frontend and backend
{% endhint %}

<details>

<summary>Generating the SDK</summary>

1. Start by navigating to the SDK portal from the navigation bar.

<img src="../.gitbook/assets/CleanShot 2024-06-12 at 11.02.38@2x.png" alt="" data-size="original">

2. You can now select from your approved modules and services. If you do not see anything, please check the steps [module-revision.md](../using-uniscale/specification/module-revision.md "mention") and [service-revisions.md](../using-uniscale/documentation/service-revisions.md "mention")

<!---->

3. Select your preferred development language

<!---->

4. Select "Save changes". This will start generating the SDK.

Read the detailed steps here: [introduction-to-sdk.md](../using-uniscale/implementation/introduction-to-sdk.md "mention")

</details>

<details>

<summary>Using the SDK</summary>

Once the SDK is generated, the instructions for how to utilize show on the screen.

Depending on how you plan to use the SDK, we have created dedicated articles to guide you:

* [library-implementation-basics](../using-uniscale/implementation/library-implementation-basics/ "mention")
* [quick-start-front-end-with-uniscale-sdk](../using-uniscale/implementation/quick-start-front-end-with-uniscale-sdk/ "mention")
* [tutorial-using-sdk-in-backend-to-handle-endpoints.md](../using-uniscale/implementation/tutorial-using-sdk-in-backend-to-handle-endpoints.md "mention")
* [tutorial-using-sdk-for-service-to-service.md](../using-uniscale/implementation/tutorial-using-sdk-for-service-to-service.md "mention")

</details>

***
