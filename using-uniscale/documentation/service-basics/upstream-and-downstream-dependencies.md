---
description: >-
  Learn how to make use of upstream and downstream dependencies. This will help
  you trace any product changes.
---

# Upstream & downstream dependencies

As your documentation grows, it can be quite hard to get an overview of its complexity. As such you might end up having questions like the following:

* "If I change this, how do I know what will break?"
* "Is it safe to change this now?"
* "Can I delete this aggregate, what if it's used somewhere?"



These are all valid day-to-day questions and to provide an answer to them, the service editor provides quick access to such dependencies.

Each of the following elements can be inspected for their dependencies via the action menu or various other quick-access UI explained below:

* Technical use cases
* Use case flows (Standalone and technical)
* Endpoints
* Aggregates
* Value Objects
* Property groups

### Upstream vs downstream

There are 2 types of dependency in software development and Uniscale:

"Who is dependent on me" - <mark style="color:purple;">**`upstream dependency`**</mark>

"What am I dependent on" - <mark style="color:purple;">**`downstream dependency.`**</mark>&#x20;



### Accessing the dependencies from the interface

Each item above that supports can be hovered and via the actions menu, upwards or downwards dependencies can be inspected.

<figure><img src="../../../.gitbook/assets/image (70).png" alt=""><figcaption></figcaption></figure>

### Understanding the dependency inspection view

<figure><img src="../../../.gitbook/assets/image (71).png" alt=""><figcaption></figcaption></figure>

When inspecting any item in any dependency mode, you will see a filtered view of the documentation or the Functional view, with only the items relevant to the dependency.&#x20;

Any item that matches that criteria is also highlighted further in a <mark style="color:purple;">Blue accent</mark> in the Overview, and also in the Main content.

<figure><img src="../../../.gitbook/assets/image (72).png" alt=""><figcaption></figcaption></figure>

The user can also show the full specification via the action at the bottom, or exit and go back to the original view from the dependencies view.

<figure><img src="../../../.gitbook/assets/image (73).png" alt=""><figcaption></figcaption></figure>



### Ruleset for each item

Each item is dependent on various items in the hierarchical order. Let's break that down per dependencies type. &#x20;

{% hint style="info" %}
Note: namespaces are always shown any of the following items located inside of them in the structure, but are not considered a dependency.&#x20;
{% endhint %}

**Upwards dependencies:**

<table><thead><tr><th width="376">Item</th><th width="421">Upwards</th></tr></thead><tbody><tr><td>Technical use cases</td><td><em><mark style="color:blue;">None</mark></em></td></tr><tr><td>Use case flows ( Standalone and technical ) </td><td>Technical Use cases &#x26;  UX flows</td></tr><tr><td>Endpoints </td><td>Use case flows</td></tr><tr><td>Data contracts ( aggregates, Value objects, Property groups)</td><td>Other data contracts &#x26; Properties</td></tr></tbody></table>

**Downwards dependencies:**

| Item                                                         | Downwards                         |
| ------------------------------------------------------------ | --------------------------------- |
| Technical use cases                                          | Technical Use case flows          |
| Use case flows ( Standalone and technical )                  | Endpoints                         |
| Endpoints                                                    | Data contracts                    |
| Data contracts ( aggregates, Value objects, Property groups) | Other data contracts & Properties |

{% hint style="info" %}
The dependencies build upon each other.

Meaning, that if I inspect upwards an endpoint, it is dependent on use case flows, which are in turn dependent on use case flows or UX flows. So the view will present the full path in that sense, contextualized to your data.
{% endhint %}



### Usage indicators

Another great helpful functionality to indicate dependencies via usage is small counter indicators on:

* use case flows
* endpoints

Clicking on them will show the upwards dependencies.&#x20;

<figure><img src="../../../.gitbook/assets/image (74).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (75).png" alt=""><figcaption></figcaption></figure>
