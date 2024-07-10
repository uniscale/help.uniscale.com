---
description: Learn the concept of service linking and the steps for doing this in Uniscale.
---

# Service linking

## Introduction

{% hint style="success" %}
This article assumes that you have covered knowledge around [specification](../../specification/ "mention") and concepts in [service-basics.md](../service-basics.md "mention").
{% endhint %}

Service linking allows you to define a service outside-in. It gives you the possibility to first define the requirements that the defined functionality has for the specified service before diving into the details of how to model the service.&#x20;

Having a look at the following illustration, we recognise the specification elements, and individually the Services on the side of it. Within the solution, there are UX flows that require functionality from the service and as such, it will be provided via Use case flows from the service.

<figure><img src="../../../.gitbook/assets/image (77).png" alt=""><figcaption></figcaption></figure>



## Tutorial: Service linking

{% hint style="info" %}
In this process, you will invite the individual responsible for the overall technical service or solution architecture. This step is crucial as it involves the initial architecture of splitting up the functionality.
{% endhint %}

***

Distribute your service functionality appropriately within your application. Many companies and projects often complicate this process, resulting in a "dependency spider web" or "ball of mud." This usually happens due to a lack of oversight on dependencies and the absence of deliberate decision



### Linking to services from solution specification

[UX flows](../../specification/solution-basics.md#ux-flow) act as the lowest level of detail you have towards the end-user behavior. They can either just describe plain end-user behavior but this is also where you define or link in the service flows that are needed to implement the use case.

<figure><img src="../../../.gitbook/assets/image (78).png" alt=""><figcaption><p>Service flow within a functional use case</p></figcaption></figure>

After being linked, the UX flow will show under the linked Service flow. With that, we mean inside the Service linking tab, which will be explained below.

<figure><img src="../../../.gitbook/assets/image (79).png" alt=""><figcaption></figcaption></figure>



### Navigate to Service linking

Please note that you will have to navigate to a module to see the "Service linking" tab.

<figure><img src="../../../.gitbook/assets/CleanShot 2024-06-18 at 10.16.01.gif" alt=""><figcaption><p>GIF: Navigate to service linking</p></figcaption></figure>



### Create service draft

You do so via the button to the right, and within the new card also create a namespace structure where the intended use case flows will be placed.

<figure><img src="../../../.gitbook/assets/CleanShot 2024-04-16 at 16.38.26.png" alt=""><figcaption></figcaption></figure>



### Link service flows&#x20;

You can now link your service flows to your service drafts. This can be done in two ways:

{% tabs %}
{% tab title="Via drag & drop in the service linking tab" %}
From the left menu bar, you can drag each&#x20;

<figure><img src="../../../.gitbook/assets/CleanShot 2024-04-16 at 16.55.26.png" alt=""><figcaption></figcaption></figure>
{% endtab %}

{% tab title="Via text command actions" %}
Click on the three dots and select "Link usecase flow":

<figure><img src="../../../.gitbook/assets/CleanShot 2024-04-16 at 16.53.33.png" alt=""><figcaption></figcaption></figure>
{% endtab %}
{% endtabs %}



### Export your service draft

Once you have processed your use case flows, you can now "distribute" , and create your services, along the nested namespaces and use case flows.

<figure><img src="../../../.gitbook/assets/image (80).png" alt=""><figcaption></figcaption></figure>

This will:

* create new Use case flows if they never existed prior.
* create new namespaces and place the Use case flows under them.
* link existing Use case flows to the UX flows in the specification.&#x20;

{% hint style="warning" %}
This change is irreversible so make sure you do this once all your specification breakdown has happened.
{% endhint %}



## Service editor functional view

Inside the service editor of a solution-owned service, the tab "Functional view" will now be active.

Here, a filtered representation of the solution specification is shown with only the items that link to the service. In essence, acting as an overview of all the dependencies the service has towards the solution.

<figure><img src="../../../.gitbook/assets/CleanShot 2024-04-16 at 16.56.52.png" alt=""><figcaption></figcaption></figure>



## Next steps

The next step in this process is to go over the technical modeling of your usecase flows, enrich them with endpoints, and model their payloads.  This is a quite complex task but we have plenty of guides to go through each step.

If you haven't done so:

* Cover the [service-basics.md](../service-basics.md "mention")
* Familiarize yourself with [upstream-and-downstream-dependencies.md](../upstream-and-downstream-dependencies.md "mention")
* Lastly, proceed to [service-revisions.md](../service-revisions.md "mention")

This should get you covered through your first revision and thus completing your first service documentation!

