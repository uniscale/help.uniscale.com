# Service Introduction

## Definition

A consensus view has evolved in the industry. Some of the defining characteristics that are frequently cited include:

* Services are organised around business capabilities.
* Services can be implemented using different programming languages, databases, hardware and software environments, depending on what fits best.
* Services are small in size, messaging-enabled, bounded by contexts, autonomously developed, independently deployable, decentralised and built and released with automated processes.
* A service CAN be independantly deployable and decentralised but also bounded context within a larger codebase.

## Standalone vs part of a solution

<figure><img src="../../.gitbook/assets/image (37).png" alt=""><figcaption></figcaption></figure>

In Uniscale, Services are created for 2 possible usages. For a solution, or as a Standalone service.

<mark style="color:purple;">**`Solution-owned-services`**</mark> are, as the name suggests, services created only to provide functionality within the bounded context of a solution. Their functionality is exposed via revisions to all the modules inside the owning solution.

<mark style="color:purple;">**`Standalone services`**</mark> are the specification of an individual service without any links into it's surrounding eco-system.
