---
description: >-
  The first dive into the specification and all its aspects: exploring the
  definition of the solution and its various elements, such as modules, pages,
  and more.
---

# Solution basics

{% hint style="info" %}
Click [here](solution-editor-overview.md) for a deep dive into the solution editor overview
{% endhint %}

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

## Solution

A solution is a term used for an end-user application or system. It intends to solve a problem for your end users. This is the top-level view of a software product.‍

In describing a solution, you are in essence defining how your software functions towards the user. What struggles in the domain does the solution seek to address and how does the solution propose to solve it?

This is also the place where you establish your team’s common understanding of your domain definitions, and the language used in the solution industry so that both the design and the services can be constructed in a language that the business can understand and evaluate.

```
// Solution structure
Solution 
├─ Module A
|   └─ Page 
|   └─ Page
|      └─ Section
|         └─ Functional use case
|             └─ UX flow
|      └─ Section
└─ Module B
```

**Examples of different solutions:**&#x20;

* A desktop application for keeping inventory of a storage space&#x20;
* A web application for organizing shifts for staff in a grocery store
* A communication system for an elementary school’s teachers and parents

<figure><img src="../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

## Module

When the description of your solution is satisfactory, your designers and product leads can start documenting the proposed designs and prototypes of the product.

A module is a functionally isolated part of the software that has distinct ownership over its functionality and revision lifecycle. Placing a boundary in the application at points where it makes sense to divide responsibilities for parts of the software.&#x20;



Examples of modules could be:

* User and account
* Payment
* Inventory
* Content management‍



Modules are specified with their functionality, the work that needs to be done within the boundaries of the module.

<figure><img src="../../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

## Page

A page represents a single screen or view that users interact with. Each page within the application can be described in the solution specification and/or functional use case, including its layout, content, navigation elements, and functionality. Additionally, wireframes or mockups may be provided to visualize the design of each page.

User Interface (UI) mockups can be uploaded for a visual reference. Both high and low-fidelity designs can work to give enough details for describing UI Flows.

<figure><img src="../../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

### Sections

A section refers to a subdivision within the document that focuses on a specific aspect of the use case. Each section provides detailed information and guidance related to that aspect, contributing to the overall clarity and comprehensiveness of the specification.&#x20;

The idea is to keep breaking them down into a structure of nested sections to define the interface.&#x20;

#### Sibling section

A section can be added on the same level as others, and we refer to them as Siblings

```
Page
- section
- section
```

#### Child/nested section

In other scenarios where your UI requires it due to complexity, you can also **nest** underneath sections under sections.

```
Page
- section
    - child section
- section
    - child section
```

<figure><img src="../../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

## Functional use case

A functional use case (UC) consists of a description where you can the high-level functionality is provided to the end user. For example:&#x20;

> The user searches for a travel destination in a search box, and the user uploads contact details to their profile.

<figure><img src="../../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

Further, it can contain more elements of the UC such as&#x20;

* UI Designer notes
* UX Product notes

<figure><img src="../../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

#### **UI Designer notes**

For every User Interface (UI) element there’s a UI designer note where your designer and product lead can describe the functionality and the restrictions you envision for that part of the UI.

An example of a UI designer note could be:

* Displayed information
* Buttons
* Areas that can expand and collapse
* Drag and drop interfaces
* Popups and triggered displays of information

You can also enrich the UI designer note with functional acceptance criteria that serve as hard boundaries for the implementation of the element. These can even be foundational for testing later on.

<figure><img src="../../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

#### UX Product notes

The UX Product notes allow you to add notes and provide a more detailed description regarding the intended user experience for a specific functional case.

#### UX flow

The UX flow represents a specific path intended for the user.

<figure><img src="../../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

### Functional acceptance criteria

A list of qualifications that the implementation of the UX flow needs to fulfill. Usually, functional details are not easily communicated through the illustrated UI.



Examples of acceptance criteria could be:

* Assurances for accessibility of variable screen types and sizes (don't show on mobile, etc)
* Front-end effects and animations  (disabled buttons, etc)
* Error handling such as password length not matching, etc



After all the UI flow’s expected behavior is documented, the functional specification should be complete. The next step is to start linking the functional specification to a set of underlying services to achieve the desired functionality.



***

<figure><img src="../../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>

### **Linked Use Cases flows**

#### **The starting point for service design in a solution**

{% hint style="warning" %}
_This part should be done by people familiar with your existing services. Like a system architect or product manager._
{% endhint %}



The UX flows within your Solution rely on functionality from the service, which will be provided through service flows.

***

### Service

A service refers to a discrete unit of functionality or capability provided by a system or application. &#x20;

Each service is defined by its inputs, outputs, behavior, and interactions with other components of the system. Describe the requirements for the underlying technical flows that will enable you to build the desired functionality.

{% hint style="info" %}
To learn more about Services, visit our detailed [Service basics](../documentation/service-basics.md) article
{% endhint %}

***

## Functionalities

<details>

<summary>Richt text editor</summary>

Our Rich text editor allows you to write your specifications using advanced styling options (heading, bold, italic, bullet points, and many more) and to embed media, images, and hyperlinks.

</details>

<details>

<summary>AI Functionality</summary>

Our AI functionality will provide your code generator with the needed domain-driven product information so you can work on your code much faster and with reduced costs.

</details>

<details>

<summary>Comments </summary>

You can also comment on different sections of your solution allowing you to add notes to the development process that can be seen and answered by your colleagues.

</details>

<details>

<summary>Commands </summary>

Uniscale offers a wide range of commands that allow you to write your specifications and build your solution in a matter of one simple click.

</details>

<details>

<summary>Share Solution</summary>

As you work on developing your solution inside Uniscale, you can also share it with your colleagues and bring in more people to work with you.

</details>



***
