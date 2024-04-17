---
description: >-
  Learn the Uniscale process of 'how-to' do module revisions and approving your
  functional specifications in the solution editor.
---

# Module revision

{% hint style="info" %}
This article assumes that you have covered knowledge around [specification](./) and concepts in [solution basics](solution-basics.md).  If not, it is recommended to follow those first in order to better understand this article.
{% endhint %}

## The module revision flow <a href="#the-module-revision-flow" id="the-module-revision-flow"></a>

Your specification is written through multiple deliveries.&#x20;

Whether you use an **agile-based**, **waterfall** or other methodology, this way of creating module revisions will allow you to iteratively build your specification.&#x20;

In this article, we will do a breakdown and tutorial of the module revision flow.&#x20;

<figure><img src="https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FGm4FsIEaw1uBtZauyirr%2Fuploads%2FQtmxO2WW8lTd8Pblkl46%2F_illustration_6.png?alt=media&#x26;token=d5927f85-7c47-41e8-8437-8032c7191dc6" alt=""><figcaption><p>The module revision cycle (writing content, readying and approving, new revisions and unlocking content)</p></figcaption></figure>

### First cycle&#x20;

* The first revision you write will take you into the "**Write content**" step.&#x20;
* In the first revision, all content is new **so there would be nothing to unlock**. However, you will still go through the **step of marking your content as ready** so that you can incrementally lock down parts of your specification.&#x20;
* When everything is marked as ready - **click the "Approve" button**, to approve the revision. This is the flow you will go through every time you want to release changes to your product.

### General process afterwards

Every revision will go through the same flow of initiating; &#x20;

* **Unlocking content** you want to change&#x20;
* **Writing/editing** content and&#x20;
* Then lastly **readying content** and **approving** it.

## Processes

### Lockable cycle&#x20;

<figure><img src="../../.gitbook/assets/image (83).png" alt=""><figcaption><p>Visual representation of the cycle of locking and unlocking content</p></figcaption></figure>

Your modules, pages, sections, functional use cases and UX flows are all subject to the locking cycle.

Exploring step by step the process, we have :&#x20;

* When a new item is created, it has the status of **`"edited"`**
* Once all requirements are met, it can now be **`"marked as ready"`**
* When the owning module is **`Approved`**, all items are moved to **`"locked"`**
* Later, when a new revision is made, all items are still in **`"locked"`**
* From here, one can manually **`"unlock"`** the items that are intended for changes, and move them to **`"unlocked"`**
* If any change is made to a **`"unlocked"`** item, it gets automatically moved to the status **`"edited"`**



### Exploration with conceptual explanation

{% tabs %}
{% tab title="Items created" %}
In the start you can have the following:

* Content that is locked (marked as locked) - finished content
* Unlocked  - edited content&#x20;
* Untouched or just not locked (marked as edited) - draft content&#x20;
* And also items in ready&#x20;

<figure><img src="../../.gitbook/assets/image (84).png" alt=""><figcaption><p>In this state, the content is finished and locked in. By pressing the "Approval" - you are creating your first revision of your solution.</p></figcaption></figure>
{% endtab %}

{% tab title="Marked as ready" %}
Further in the process, your work is finished and you aim to wrap things up as you go.

* Items are gradually moved toward a Ready state

<figure><img src="../../.gitbook/assets/image (85).png" alt=""><figcaption><p>Content marked as ready for "locking"</p></figcaption></figure>
{% endtab %}

{% tab title="Locked & approved" %}
When all content is approved, all items are locked (in 'Rev 1.0)&#x20;

From here on, you can start a new revision

<figure><img src="../../.gitbook/assets/image (86).png" alt=""><figcaption><p>Locked content in 'Rev 1.0'. </p></figcaption></figure>
{% endtab %}

{% tab title="Unlocking for a new revision" %}
Once a new revision (1.1) is made, that is reflected in the revision number.

When starting a new revision - all content will ALWAYS start locked

<figure><img src="../../.gitbook/assets/image (87).png" alt=""><figcaption></figcaption></figure>
{% endtab %}

{% tab title="Repeat" %}
In your new revision, 'Rev 1.1' you have to manually unlock the content you want to change. Looping the flow to step 1.

<figure><img src="../../.gitbook/assets/image (88).png" alt=""><figcaption></figcaption></figure>
{% endtab %}
{% endtabs %}



## Interface walkthrough

Up next, we will illustrate the above cycle with interface screenshots and examples.

{% hint style="info" %}
When utilizing services in your solution, service documentation occurs between content readiness and approval.&#x20;
{% endhint %}

### Unlocking and readying <a href="#unlocking-and-readying" id="unlocking-and-readying"></a>

When you start a new revision, everything is initially locked, meaning you haven't decided to make changes yet. To make changes, you must unlock the elements first. This helps you track what you've changed or plan to change.

Filters let you focus on unlocked or changed elements, especially useful as your specification grows. Unlocking can serve as an agreement with stakeholders on intended changes. Use it to track changes and align expectations.

Similarly, you can use readiness to track what's complete and what's left in your specification. Locking down parts of your specification as you progress helps you approach completion systematically.

<figure><img src="../../.gitbook/assets/CleanShot 2024-04-12 at 16.19.19.gif" alt=""><figcaption><p>GIF: Staring a new revision, unlocking page content, editing and approving revision</p></figcaption></figure>

### Approval <a href="#approval" id="approval"></a>

For approval, if you're defining services, complete service revisions before approval. If you're only using functional specifications, you'll approve the specification after everything is marked ready. Once approved, the specification is locked, and you can start new revisions in the future.

For each module in your solution editor, you can work with the current revision and look back at any of your older revisions. In this way, you have a complete overview of the product intention and decision history.&#x20;

{% hint style="info" %}
When using "**`Mark as ready`**" or "**`Mark as unready`**" you can lock and unlock content bit-by-bit or bulk content within the editor. This can be useful if some parts are finished or more than one person is working on the same solution. See the how-to in GIF below:
{% endhint %}

<figure><img src="../../.gitbook/assets/CleanShot 2024-04-12 at 16.08.50.gif" alt=""><figcaption><p>GIF: Where to find previous module revisions </p></figcaption></figure>

{% hint style="info" %}
By pressing "Approve" you generate a new revision and save the entire solution&#x20;
{% endhint %}

***

## Summary of module revision flow   <a href="#conclusion" id="conclusion"></a>

You iteratively define your module's functionality by starting, specifying, and approving revisions in your module. You can use unlocking to align with stakeholders on what is expected to change existing functions. You can also use readying as a way of tracking your progress against completing your revision. Through multiple iterations and gradually adding functionality to your solutions modules the specification will be the single source of truth for all intentions and decisions making your product what it is today. Through the module revision history, you can go back in time and look at all your historical decisions.

#### Want more of a deep dive? Watch this video and see the module flow process exemplified:&#x20;

{% embed url="https://youtu.be/Bc3auFzvn10" %}
Video explainer&#x20;
{% endembed %}
