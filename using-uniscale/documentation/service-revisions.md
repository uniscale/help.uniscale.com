---
description: Learn the concept and steps for service revisions.
---

# Service revisions

## Introduction

With Uniscale, you can create revisions for each service, allowing you to compare revisions and get a historical overview of changes. Furthermore, your revisions will have their own approval flow.

<figure><img src="../../.gitbook/assets/CleanShot 2024-07-29 at 14.21.32.png" alt=""><figcaption><p>Service editor: Changelog</p></figcaption></figure>

In this article, we will explore two areas:

* [#service-locking-and-approving](service-revisions.md#service-locking-and-approving "mention"): Learn how to utilize this functionality.
* [#concept-service-revision](service-revisions.md#concept-service-revision "mention"): Understand the concept behind revisions.



## How to: Service revisions <a href="#service-locking-and-approving" id="service-locking-and-approving"></a>

### Service locking and approving <a href="#service-locking-and-approving" id="service-locking-and-approving"></a>

You will lock and approve each service revision as you want to keep track of your changes over time.

<figure><img src="../../.gitbook/assets/CleanShot 2024-07-29 at 14.36.47.gif" alt=""><figcaption><p>Service editor: Ready and approve revision</p></figcaption></figure>

1. Select "Ready all"
2. In the overview, select "Set all to ready"
3. Select "Approve"
   1. Give your revision a title. Note that it will automatically get a version number.
   2. Optional: Add a description.
   3. Click "Submit"

{% hint style="info" %}
Once you have approved a revision, you can head to the SDK Portal to generate an updated SDK: [#generating-the-sdk](../implementation/introduction-to-sdk/#generating-the-sdk "mention")
{% endhint %}



### Create a new revision

<figure><img src="../../.gitbook/assets/CleanShot 2024-07-29 at 14.37.20.png" alt=""><figcaption><p>Service editor: Start new revision</p></figcaption></figure>

To start a new revision:

1. Click "Start new revision"
2. Give your revision a title. Note that it will automatically get a version number.
3. Optional: Add a description.
4. Click "Submit"



### Service changelog

To view the changelog, click the "clock" icon in the upper right corner.

<figure><img src="../../.gitbook/assets/CleanShot 2024-07-29 at 14.44.44.gif" alt=""><figcaption><p>Service editor: Changelog</p></figcaption></figure>

You can select and compare each of your revisions and get an overview of all changes.

Each color will represent the type of change:

* <mark style="color:green;">Green</mark>: Added
* <mark style="color:purple;">Purple</mark>: Modified
* <mark style="color:red;">Red</mark>: Deleted



### Explore previous revisions

To explore each of your previous service revisions, click on the name of your revision in the upper right corner.&#x20;

<figure><img src="../../.gitbook/assets/CleanShot 2024-07-29 at 14.49.20.png" alt=""><figcaption><p>Service editor: Previous revisions</p></figcaption></figure>

***

## Concept: Service revision

Within the cycles of modeling and producing well-written documentation, you will find yourself completing items and getting them to a stage where you can lock things in place before a revision.

To do so in a better manner, we have provided each item in your documentation with its lifecycle related to its meaning.

For that, we distinguish between:

* Items to be reused (endpoints, data contracts, properties).
* items that are single declarations (namespaces, Use case flows, Technical use cases)

<details>

<summary>Listing the structure of a service, we can have the following items:</summary>

* namespaces
* technical use cases
* use case flows
* endpoints
* data contracts
  * aggregates
  * value objects
  * property groups&#x20;
  * properties

For a more detailed breakdown, read [service-basics](service-basics/ "mention")

</details>



Each item is subjected to a lifecycle, with different meanings.

<figure><img src="../../.gitbook/assets/image (60).png" alt=""><figcaption></figcaption></figure>



### Completion cycle

<figure><img src="../../.gitbook/assets/image (61).png" alt=""><figcaption></figcaption></figure>

Endpoints, data contracts, and properties are considered items that are agnostic of the entire status of the service. As a whole, they can be "completed" before the overall approval status and as such, their cycle reflects their state of being "done" or "completed".

Exploring step by step the process, we have:

* When a new item is created, it is in the status of "**`draft`**"
* Afterward, with new changes done, it goes into "**`edited`**"
* Once all the conditions are met, the item can be "**`completed`**"
* Once completed, the item can be **`"opened"`** to new changes
* If some changes are made, then the item is moved back into **`"Edited"`**

### Lockable cycle

<figure><img src="../../.gitbook/assets/image (62).png" alt=""><figcaption></figcaption></figure>

Namespaces, technical use case flows, and use case flows are all process items that are relevant to the end goal of the service. As such, rather than a completion intention, they have a "is this final", or "is this locked" cycle.



Exploring step by step the process, we have:&#x20;

* When a new item is created, it has the status of **`"edited"`**
* Once all requirements are met, it can now be **`"marked as ready"`**
* When the owning module is **`Approved`**, all items are moved to **`"locked"`**
* Later, when a new revision is made, all items are still in **`"locked"`**
* From here, one can manually **`"unlock"`** the items that are intended for changes, and move them to **`"unlocked"`**
* If any change is made to a **`"unlocked"`** item, it gets automatically moved to the status **`"edited"`**



### Approval of the service & revisions

Service approval is a collation of all the above processes and loops. Let's take a conceptual example of that scenario, with images to visually represent the state at all times.

1. In the start, the service grows to a stage where various items will be in either the **`"locking lane"`** or the **`"completion lane"`** . This is further expanded with dependencies between the 2 types, in our example in a simple, upwards dependencies manner.

<figure><img src="../../.gitbook/assets/image (63).png" alt=""><figcaption></figcaption></figure>

2. As things progress in the service modeling, all items are now **`completed`** and the process items are **`ready to be locked.`**

<figure><img src="../../.gitbook/assets/image (64).png" alt=""><figcaption></figcaption></figure>

3. With everything in place, the service has now been approved, and Revision 1.0 has been created. This means all items are moved to **`locked`** state and the others remain **`completed`**.

<figure><img src="../../.gitbook/assets/image (65).png" alt=""><figcaption></figcaption></figure>

4. From here on, of course, the service will grow towards a new revision, and to initiate one, the service will need to be opened, and various items will be **`unlocked.`** As such, all items that are downward dependencies of such items will be marked as **`Opened`**, marking the intent to add changes. Once changes are made, the cycle goes back to step 1 in this guide.

<figure><img src="../../.gitbook/assets/image (66).png" alt=""><figcaption></figcaption></figure>



### Service timeline

Over time the service will receive many revisions, all needed incremental changes. This is expected and is a sign of an ever-growing service (in quality and overview of usage, and not primarily in size).

<figure><img src="../../.gitbook/assets/image (69).png" alt=""><figcaption></figcaption></figure>
