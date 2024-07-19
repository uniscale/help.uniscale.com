---
description: Learn the concept and steps for service revisions.
---

# Service revisions

## Introduction to process

Within the cycles of modeling and producing well-written documentation, you will find yourself completing items and getting them to a stage where you can lock things in place before a revision.

To do so in a better manner, we have provided each item in your documentation with its lifecycle related to its meaning.



For that, we distinguish between:

* "items" that are to be reused (endpoints, data contracts, properties).
* items that are single declarations (namespaces, Use case flows, Technical use cases)

As a whole, a service has revisions and is approved. This is symbolized via the revisions dropdown where you can see a list of your past revisions titles and numbers.



Listing the structure of a service, we can have:

* namespaces
* technical use cases
* use case flows
* endpoints
* data contracts
  * aggregates
  * value objects
  * property groups&#x20;
  * properties

{% hint style="info" %}
For a more detailed breakdown, read [service-basics](service-basics/ "mention")
{% endhint %}

Each of them is subjected to a lifecycle, with different meanings.

<figure><img src="../../.gitbook/assets/image (60).png" alt=""><figcaption></figcaption></figure>

## Processes

### Completion cycle

<figure><img src="../../.gitbook/assets/image (61).png" alt=""><figcaption></figcaption></figure>

Endpoints, data contracts, and properties are considered items that are agnostic of the entire status of the service. As a whole, they can be "completed" before the overall approval status and as such, their cycle reflects their state of being "done" or "completed".

Exploring step by step the process, we have :

* When a new item is created, it is in the status of "**`draft`**"
* Afterward, with new changes done, it goes into "**`edited`**"
* Once all the conditions are met, the item can be "**`completed`**"
* Once completed, the item can be **`"opened"`** to new changes
* If some changes are made, then the item is moved back into **`"Edited"`**

### Lockable cycle

<figure><img src="../../.gitbook/assets/image (62).png" alt=""><figcaption></figcaption></figure>

Namespaces, technical use case flows, and use case flows are all process items that are relevant to what the end goal of the service is. As such, rather than a completion intention, they have a "is this final", or "is this locked" cycle.



Exploring step by step the process, we have:&#x20;

* When a new item is created, it has the status of **`"edited"`**
* Once all requirements are met, it can now be **`"marked as ready"`**
* When the owning module is **`Approved`**, all items are moved to **`"locked"`**
* Later, when a new revision is made, all items are still in **`"locked"`**
* From here, one can manually **`"unlock"`** the items that are intended for changes, and move them to **`"unlocked"`**
* If any change is made to a **`"unlocked"`** item, it gets automatically moved to the status **`"edited"`**



## Approval of the service & revisions

Service approval is a collation of all the above processes and loops. Let's take a conceptual example of that scenario, with images to visually represent the state at all times.

1. In the start, the service grows to a stage where various items will be in either the **`"locking lane"`** or the **`"completion lane"`** . This is further expanded with dependencies between the 2 types, in our example in a simple, upwards dependencies manner.

<figure><img src="../../.gitbook/assets/image (63).png" alt=""><figcaption></figcaption></figure>

2. As things progress in the service modeling, all items are now **`completed`** and the process items are **`ready to be locked.`**

<figure><img src="../../.gitbook/assets/image (64).png" alt=""><figcaption></figcaption></figure>

3. With everything in place, the service has now been approved, and Revision 1.0 has been created. This means all items are moved to **`locked`** state and the others remain **`completed`**.

<figure><img src="../../.gitbook/assets/image (65).png" alt=""><figcaption></figcaption></figure>

4. From here on, of course, the service will grow towards a new revision, and to initiate one, the service will need to be opened, and various items will be **`unlocked.`** As such, all items that are downward dependencies of such items will be marked as **`Opened`**, marking the intent to add changes. Once changes are made, the cycle goes back to step 1 in this guide.

<figure><img src="../../.gitbook/assets/image (66).png" alt=""><figcaption></figcaption></figure>



## Revisions

Revisions represent changes done to your service with the intent to release functionality around your projects. Revisions can be as big or as small as you need.&#x20;

In the interface, any revision looks like the following:

<figure><img src="../../.gitbook/assets/image (67).png" alt=""><figcaption></figcaption></figure>

Each revision will be given a name when created and a description. This can be edited until the revision is approved at the end.

<figure><img src="../../.gitbook/assets/image (68).png" alt=""><figcaption></figcaption></figure>

### Service timeline

Over time the service will receive many revisions, all needed incremental changes. This is expected and is a sign of an ever-growing service (in quality and overview of usage, and not primarily in size).

<figure><img src="../../.gitbook/assets/image (69).png" alt=""><figcaption></figcaption></figure>
