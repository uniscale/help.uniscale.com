# Advanced concepts

## Defining module boundaries

Creating clear and effective module boundaries is important for your organization. A module is a functionally isolated part of the software that has distinct ownership over its functionality and revision lifecycle.&#x20;

Placing a boundary in the application at points where dividing responsibilities for parts of the software makes sense.&#x20;



### Modules to follow your product structure

To maintain optimal functionality and ease of updates in your application, it is crucial to structure your modules so that any changes are typically confined to a single module.

As the specification progresses through incremental module revisions, it is essential to view each module revision as its own project or delivery. Segregate your modules in such a way that the majority of project or delivery changes remain within a single module. In short, elements that evolve together should be grouped together.



### Organize modules based on ownership

You would want a single team to own the entire module. The reasoning is that you want to avoid shared ownership of a module as you then will quickly end up with projects/releases that are executed separately but are tightly coupled to each other and end up having to be released together anyway.

The way you define your module boundaries allows you to decide how you want to grow your organization in the future as the organization of functionality through module and service boundaries will impact the future structure of the organization maintaining them.

<figure><img src="../../.gitbook/assets/CleanShot 2024-04-26 at 15.07.50.png" alt=""><figcaption></figcaption></figure>

***

## Setting service boundaries

The service boundaries are governed through much of the same thinking as the module boundaries. As services just like modules are maintained through revisions, it is important that a single team has ownership of a service and that functionality that normally changes together is contained by a single service.&#x20;

The reasoning is that you want to avoid shared ownership of a service as you then will quickly end up with projects/releases that are executed separately but are tightly coupled to each other and end up having to be released together anyway.

In Uniscale you do not necessarily have to think of a single service as a single source code or a hosted instance of a source code. Through the SDK you may work with monoliths containing multiple services in one hosted instance and a single service divided into multiple running source bases. This allows you to split your service based on functionality while still having the flexibility to scale and maintain a good, clean, and flexible technical architecture.

The way you define your service boundaries allows you to decide how you want to grow your organization in the future as the organization of functionality through module and service boundaries will impact the future structure of the organization maintaining them.



### Defining service boundaries

Through Uniscale you essentially have two ways of defining your service boundaries. One is the traditional inside-out where you define the functionality from within the services themselves. This can often lead to defining too much functionality and often also defining misaligned functionality. In Uniscale even this approach will lead to more accurate service boundary modeling as you will always start by defining your standalone and technical use case flows.&#x20;

This forces you to define why you need the functionality ahead of defining the endpoints themselves. As a result, you are much more equipped to detect any bad service boundary definitions before it's too late.

The recommended way when using the functional specification in Uniscale is to model your service functionality through service linking. This means using the functional requirements to define what functionality is required from the services



### Service boundaries through Service Linking

Through this flow you will first go through all defined UX flows in your specification and define which ones require functionality from a service. If the functionality exists in the service from before, you can just go ahead and find it in the services tab in the left sidebar and drop it onto the UX flow.

However, if the functionality does not exist in a service yet, you define a service flow under the UX flow and write a short description of what it needs to do and what its technical acceptance criteria are. You will not decide at this point which service you want to have delivered this flow.

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

When you have gone through and mapped up all UX flows in the current module revision to existing or new service flows, it is time to move over to the Service Linking tab. The Service Linking tab allows you to map your newly defined service flows to any existing or new services while having the full perspective in mind.&#x20;

This will allow you to see the larger picture as you split the functionality out between services potentially owned by multiple teams in your organization. This allows you already here to realize whether you will need to engage more than one team to implement the specified functionality and what impact that will have on your project.

{% hint style="info" %}
Any new dragged or connected Service flows to a service will show up with a Blue accent, to indicate change. This is also reflected in the button label under each service.
{% endhint %}

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

Once all service flows have been connected to a service, the list will be empty.&#x20;

You can enable to see the linked ones as well via the top filter. You are now ready to create any new services that you have designed and export the changes to any existing services. By exporting you will start a new revision of the service and prepare it will all the newly defined flows.

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption><p>The service linking tab after all service flows have been linked</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/CleanShot 2024-04-26 at 13.25.30.png" alt=""><figcaption><p>The filtering options in the left side of service linking page</p></figcaption></figure>



