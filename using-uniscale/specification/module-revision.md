---
description: >-
  Learn the Uniscale process of 'how-to' do module revisions and approving your
  functional specifications in the solution editor.
---

# Module revision

{% hint style="success" %}
This article assumes that you have covered knowledge around [.](./ "mention") and concepts like [solution-basics.md](solution-basics.md "mention")
{% endhint %}



## Introduction to module revisions <a href="#the-module-revision-flow" id="the-module-revision-flow"></a>

{% hint style="info" %}
A solution consists of modules, each having its own revision and approval flow.
{% endhint %}

As your product develops, your specification is written through multiple deliveries.&#x20;

Whether you use agile, waterfall, or other methodologies, this way of creating module revisions will allow you to iteratively build your specification.&#x20;

<figure><img src="https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FGm4FsIEaw1uBtZauyirr%2Fuploads%2FQtmxO2WW8lTd8Pblkl46%2F_illustration_6.png?alt=media&#x26;token=d5927f85-7c47-41e8-8437-8032c7191dc6" alt=""><figcaption><p>Illustration of the module revision cycle.</p></figcaption></figure>

### The four phases of module revisions

Every revision will go through the same flow of initiating; &#x20;

* **Write content:** Update, remove, or add new content.
* **Ready and Approve:** Lock in your new changes.
* **New revision:** To make a change, create a new revision.
* **Unlock content** that you want to change.&#x20;



### Lockable cycle

<figure><img src="../../.gitbook/assets/image (83).png" alt=""><figcaption><p>Illustration of the cycle of locking and unlocking content</p></figcaption></figure>

Your modules, pages, sections, functional use cases, and UX flows are all subject to the locking cycle.

Exploring step by step the process, we have:&#x20;

* When a new item is created, it has the status of **`"edited"`**
* Once all requirements are met, it can now be **`"marked as ready"`**
* When the owning module is **`"Approved"`**, all items are moved to **`"locked"`**
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

When starting a new revision - all content will always start as locked.

<figure><img src="../../.gitbook/assets/image (87).png" alt=""><figcaption></figcaption></figure>
{% endtab %}

{% tab title="Repeat" %}
In your new revision, 'Rev 1.1' you have to manually unlock the content you want to change. Looping the flow to step 1.

<figure><img src="../../.gitbook/assets/image (88).png" alt=""><figcaption></figcaption></figure>
{% endtab %}
{% endtabs %}



## How to: Module revisions

{% hint style="info" %}
When utilising services in your solution, service documentation occurs between content readiness and approval.&#x20;
{% endhint %}



### Edit an existing module

{% tabs %}
{% tab title="Select a module" %}
1. Click on the name of your solution in the upper left corner.
2. Select a module.

<figure><img src="../../.gitbook/assets/CleanShot 2024-06-17 at 14.15.08@2x.png" alt=""><figcaption><p>Illustration of how to select a module</p></figcaption></figure>
{% endtab %}

{% tab title="Create a new revision" %}
1. Click on "Start new revision"&#x20;
2. Give your revision a title
3. Write a short description
4. Select "Start new revision"

<figure><img src="../../.gitbook/assets/CleanShot 2024-06-17 at 14.20.09@2x.png" alt=""><figcaption></figcaption></figure>
{% endtab %}

{% tab title="Unlock elements" %}
1. Unlock each element that you want to edit
2. You can now edit the content.

<figure><img src="../../.gitbook/assets/CleanShot 2024-06-17 at 14.32.42@2x.png" alt=""><figcaption><p>Illustration of how to unlock an element.</p></figcaption></figure>
{% endtab %}
{% endtabs %}



### Approve a new module revision

{% tabs %}
{% tab title="Ready all at once" %}
When you are done editing your module revision you will begin to approve your new revision.&#x20;

This option will allow you to manually select multiple items and ready at once.

1. Click on "Ready all"
2. Select desired items.
3. Click "Set all to ready".

<figure><img src="../../.gitbook/assets/CleanShot 2024-06-17 at 14.44.04@2x.png" alt=""><figcaption><p>Illustration of "Ready all"</p></figcaption></figure>
{% endtab %}

{% tab title="Ready individually" %}
1. In the filter bar, navigate to "Unlocked & Edited". This will only show edited content.
2. Go through each item and click on "Mark as ready"
3. Select either "Only item" or "Mark as ready (with children)"

<figure><img src="../../.gitbook/assets/CleanShot 2024-06-17 at 16.08.17.png" alt=""><figcaption><p>Illustration of "Ready" an item</p></figcaption></figure>
{% endtab %}

{% tab title="Approve" %}
With all items marked as ready, you are ready to approve your module revision:

{% hint style="info" %}
If you are defining services, complete service revisions before approval.&#x20;
{% endhint %}

1. Click "Approve"
2. Give your revision a title and description
3. Click "Save and approve revision"

<figure><img src="../../.gitbook/assets/CleanShot 2024-06-17 at 16.11.50.png" alt=""><figcaption></figcaption></figure>
{% endtab %}
{% endtabs %}



## Explore previous revisions

You can look up all previous revisions to compare your content

1. Select a specific module
2. Click on the dropdown and get a list of all revisions

<figure><img src="../../.gitbook/assets/CleanShot 2024-06-17 at 16.15.29.png" alt=""><figcaption><p>Module revision overview</p></figcaption></figure>

***

## Summary of module revision flow   <a href="#conclusion" id="conclusion"></a>

You iteratively define your module's functionality by starting, specifying, and approving revisions in your module. You can use unlocking to align with stakeholders on what is expected to change existing functions. You can also use readying as a way of tracking your progress against completing your revision. Through multiple iterations and gradually adding functionality to your solutions modules the specification will be the single source of truth for all intentions and decisions making your product what it is today. Through the module revision history, you can go back in time and look at all your historical decisions.

#### Want more of a deep dive? Watch this video and see the module flow process exemplified:&#x20;

{% embed url="https://youtu.be/Bc3auFzvn10" %}
Video explainer&#x20;
{% endembed %}
