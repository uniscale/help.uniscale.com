# Service Linking

This article assumes that you have covered knowledge around [specification](../specification/) and concepts in [service basics](service-basics.md).  If not, it is recommended to follow those first to better understand this article.

Service linking allows you to start defining your service outside in. It gives you the possibility to first define the requirements that the defined functionality has to the specified service before diving into the details on how to model the service. Having a look at the following illustration, we recognise the specification elements, and individually the Services on the side of it.&#x20;

<figure><img src="../../.gitbook/assets/image (76).png" alt=""><figcaption></figcaption></figure>

Within the solution, there are UX flows that require functionality from the service and as such, it will be provided via Use case flows from the service.&#x20;

<figure><img src="../../.gitbook/assets/image (77).png" alt=""><figcaption></figcaption></figure>

The process is more detailed than this so let's break it down with interface examples.&#x20;

### Defining the services process&#x20;

In this process, you'll invite the individual responsible for the overall technical service or solution architecture. This step is crucial as it involves the initial architecture of splitting up the functionality.

***

In essence, distributing your service functionality where it belongs in your application. This is where most of the time, many companies and projects end up going the complicated route and create what we call a "dependency spider web" or "a ball of mud". This is done due to a lack of an overview of the dependencies and also conscious decisions behind each of them.&#x20;

### Linking to services from solution specification

[UX flows](../specification/solution-basics.md#ux-flow) acts as the lowest level of details you have towards the end user behaviour. They can either just describe plain end user behaviour but this is also where you define / link in the service flows that is needed to implement the use case.

<figure><img src="../../.gitbook/assets/image (78).png" alt=""><figcaption></figcaption></figure>

After being linked, the UX flow will show under the linked Service flow. With that we mean inside the Service linking tab, which will be explained bellow.

<figure><img src="../../.gitbook/assets/image (79).png" alt=""><figcaption></figcaption></figure>

Once a Service flow is linked (and this process is repeated from many other UX flows), from within the Service linking tab, you can now export all changes, service by service. This can happen in the UI in 2 ways:

* **Via text command actions**

<figure><img src="../../.gitbook/assets/CleanShot 2024-04-16 at 16.53.33.png" alt=""><figcaption></figcaption></figure>

* **Via drag & drop in the service linking tab**

<figure><img src="../../.gitbook/assets/CleanShot 2024-04-16 at 16.55.26.png" alt=""><figcaption></figcaption></figure>



### Within the Service linking tab

The user is first met with a list of use case flows that needs to be placed in services.&#x20;

<figure><img src="../../.gitbook/assets/CleanShot 2024-04-16 at 16.40.25.png" alt=""><figcaption></figcaption></figure>

The services can be either already existing or new ones have to be drafted.

You do so via the button to the right, and within the new card also create a namespace structure where the intended use cases flows will be placed.

<figure><img src="../../.gitbook/assets/CleanShot 2024-04-16 at 16.38.26.png" alt=""><figcaption></figcaption></figure>

Once you have processed your use case flows, you can now "distribute" , and create your services, along the nested namespaces and use case flows.

<figure><img src="../../.gitbook/assets/image (80).png" alt=""><figcaption></figcaption></figure>

This will:

* create new Use case flows if they never existed prior
* create new namespaces and place the Use case flows under them
* link existing Use case flows to the UX flows in the specification.&#x20;

{% hint style="warning" %}
This change is irreversible so make sure you do this once all your specification breakdown has happened.
{% endhint %}

## Service editor functional view

Inside the service editor of a solution-owned service, the tab called Functional View will now be active.

Inside, a filtered representation of the solution specification is shown with only the items that link to the service. In essence, acting as an overview of all the dependencies the service has towards the solution.

<figure><img src="../../.gitbook/assets/CleanShot 2024-04-16 at 16.56.52.png" alt=""><figcaption></figcaption></figure>

Next step in this process is to now go over the technical modelling of your usecase flows, meeting them with endpoints, modell their payloads.  This is a quite complex task but we have plenty of guides to go through each step.

If you havent done so:

* [cover the basics of service](service-basics.md)
* [familiarise yourself with the upstream and downstream dependencies](upstream-and-downstream-dependencies.md)
* [and lastly learn about service revisions](service-revisions.md)

This should get you covered through your first revision and thus completing your first service documentation!

