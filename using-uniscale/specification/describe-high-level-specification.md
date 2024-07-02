---
description: Learn how to describe your high-level specification along with best practices.
---

# Describe high-level specification

{% hint style="info" %}
Before kick-starting your Uniscale journey you should have:

1. [Create an account](https://help.uniscale.com/account-and-preferences/create-an-account)
2. [Create a workspace](https://help.uniscale.com/workspace-administration/manage-workspaces/create-a-workspace)
3. [Invite to a workspace](https://help.uniscale.com/workspace-administration/manage-workspaces/invite-to-a-workspace)

When this is done, you are ready to follow the guide below on how to build better software!
{% endhint %}



## Introduction to high-level specification

The specification, or functional requirement specification, is where you specify the overall idea. This includes an introduction, the main challenge, why you are going to solve this, and on a high level your approach to solving this.

{% hint style="info" %}
This part is done from an abstract view, meaning that it is not about solving the actual problem, but rather carefully explaining what the problem is and what the desired outcome is.
{% endhint %}

This is typically defined by the Founder, Visionary, Product Owner, or someone who understands the solution.



### Best practice when describing your high-level specification

{% hint style="success" %}
Cater to your audience

Aim for a short and concise description. Cater the message to your audience whether this is for internal or external stakeholders.

Tip: Make use of our Generative AI to help improve your writing. Learn more here: [tutorial-using-ai-in-specification.md](tutorial-using-ai-in-specification.md "mention")
{% endhint %}

{% hint style="success" %}
Keep it at an abstract level

Focus on describing the key challenge and purpose of your specification and leave the concrete steps to solving the issue for later. This will help you make sure that people are aligned on the overall goals and that your solution will meet the customer's requirements.
{% endhint %}



## Describe your high-level specification

{% embed url="https://www.youtube.com/watch?index=1&list=PL5utFq0uexyGOAVoZxLdRIG6ti7yXqlbs&v=xtzqXVHMjpM" %}
Video: Tutorial: High-level specification
{% endembed %}

To help you get started, here are some inspirations for what to include in your specifications:

<details>

<summary>What - Describe what you're building</summary>

* Short description: Explain in a few sentences what your product is doing.
* What are the high-level functionalities and features of your solution?
  * Come up with 3-5 bullets that explains overall what your solution will be doing.
  * What are the main requirements from your actors?
  * Try to write in a few sentences how you will solve this problem without going into detail.

<img src="../../.gitbook/assets/image (100).png" alt="Template - &#x22;What is our solution?&#x22;" data-size="original">

</details>

<details>

<summary>Why - Purpose and motivation: Why are you building this solution?</summary>

Describe to your audience what the purpose of your solution is.

* What is the purpose
* What value does it bring?
* What are the desired outcomes that you want to achieve?
* What is your motivation for building this solution?
* What are the struggles and challenges that you see for example in the market?
* What are the problems or needs that people have?
* Why are we the right people to solve this problem compared to others?

![Template - "Why are we building this solution?"](<../../.gitbook/assets/CleanShot 2024-07-02 at 09.04.55.png>)

</details>

<details>

<summary>Who - Roles that will be using our solution</summary>

Start by listing all the actors that will be involved in your solution. Here is some inspiration:

* Different roles and personas
* Partners
* Distributors

Now can you group the listed actors based on eg. their type and interactions with each functionality?&#x20;

This is to identify patterns of your actors, like roles and people that interact with the solution, for example, the end-users (customers), and stakeholders like system administrators, suppliers, third-party contributors, etc.&#x20;

![Template - "Who are the actors of this solution?"](<../../.gitbook/assets/CleanShot 2024-07-02 at 09.42.47.png>)

</details>

<details>

<summary>Data sources - Where does your data come from?</summary>

List here where the different types of data will come from. Here is some inspiration:

* Manually inputting data
* Integration with systems or service providers
* Does the customer have to provide their details or personal information?



</details>



## Create and describe your first modules

{% hint style="info" %}
Before creating modules, we recommend reading our guide for best practices: [#best-practices-for-creating-modules](solution-basics.md#best-practices-for-creating-modules "mention")
{% endhint %}

<details>

<summary>Module description</summary>

The description of your module is where you describe the purpose and intention for this specific module.&#x20;

💡 Tip: You can re-use the relevant information you described in your high-level specification.

Here are relevant things to include:&#x20;

* Intended functionality for the specific module.
* What is the exact action that this module intends to achieve?
* Detailed explanation of what this module is supposed to do and how it proposes to achieve it
* Actors: Who is going to interact with this module?

![Template - Module Description](<../../.gitbook/assets/CleanShot 2024-07-02 at 10.01.51.png>)

</details>

<details>

<summary>Break your modules into pages for grouping functionality</summary>

Pages are an element for structure, where you can organize and group your functional use cases. Often used (if needed) when you have locked in the first revision.&#x20;

![Template - Pages](<../../.gitbook/assets/CleanShot 2024-07-02 at 10.02.58.png>)

You can read more about Pages here: [#page](solution-basics.md#page "mention")

</details>

<details>

<summary>Functional use cases - high level definition &#x26; user story </summary>

* This is the high-level behavior: a clear description of the high-level functionality intended for the user (this usually entails an action/ taking the user from point A to point B
* A good logic to follow is that you should describe the functional use case with:&#x20;
  * Define the actor and their needs.
  * Describe what each actor wants to achieve.
  * Define their desired outcome.
* Examples: House cleaning app: As a house owner, when my house is dirty, I want to book a cleaner, so that my house is cleaned.

![Template - Functional use cases](<../../.gitbook/assets/CleanShot 2024-07-02 at 10.04.56 (1).png>)

You can read more here: [#functional-use-case](solution-basics.md#functional-use-case "mention")

</details>

<details>

<summary>Add Acceptance criteria to your Functional use cases</summary>

* Describe what this is and how it will work
* Note; Our Generative AI can help write suggestions for what acceptance criteria to include: [#ai-generated-acceptance-criteria](tutorial-using-ai-in-specification.md#ai-generated-acceptance-criteria "mention")
* Definition: a list of qualifications that the functional use case (UX flow if detailed specification?) needs to fulfill

![Template - Acceptance Criteria](<../../.gitbook/assets/CleanShot 2024-07-02 at 10.05.54.png>)

</details>

***



## Next steps

* You can already now choose to approve your first revision: [module-revision.md](module-revision.md "mention")
* Involve your product designer and begin the [describe-detailed-specification.md](describe-detailed-specification.md "mention")
