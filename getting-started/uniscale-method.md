---
description: >-
  Discover the Uniscale Method and how to effectively leverage our approach
  throughout the software development journey.
---

# Uniscale Method

## Introduction

{% hint style="info" %}
Before reading this article, we recommend watching our brief video introduction: [#what-is-uniscale](../#what-is-uniscale "mention")
{% endhint %}

The Uniscale Method uses a systematic breakdown approach that allows you to utilize domain-driven AI. This ensures that problems are accurately identified and solutions are cost-effective.\
\
By using this method, you'll understand the reasoning behind Uniscale and the different stages of software development. This gives you a framework to break a specification down across multiple roles into a single source of truth.\
\
Each stage has its own requirements, details, and results. Understanding these is crucial for your software development journey, helping you build the right product on your first try.

<div data-full-width="true">

<figure><img src="../.gitbook/assets/CleanShot 2024-07-10 at 10.15.00.png" alt=""><figcaption><p>Phases of the Uniscale Method</p></figcaption></figure>

</div>



## Uniscale Method

### Specification

The specification, also known as “Functional Requirement Specification”, is where you describe the solution's intended capabilities, appearance, and interactions with users.

<table><thead><tr><th width="118"></th><th width="330">High level - Abstract</th><th>Detailed - Concrete</th></tr></thead><tbody><tr><td>What</td><td><p>High-level overview and introduction of your product:</p><ul><li>Abstract specification</li><li>Purpose and motivation</li><li>High-level requirements</li><li>High-level end-user behaviour</li><li>Overview of actors</li><li>Structure breakdown</li></ul></td><td><p>Moving from abstract to concrete thinking:</p><ul><li>Decide the overall approach to your solution.</li><li>Concrete user interface.</li><li>UX requirements.</li><li>UI requirements.</li></ul></td></tr><tr><td>Why</td><td>Align all stakeholders on what you are building and the purpose while serving as a reference point for your solution.</td><td>The detailed specification guides all UI and UX design aspects, forming the user experience foundation.</td></tr><tr><td>Who</td><td>Product Owner or someone with a deep understanding of the product.</td><td>UX/UI Designer</td></tr><tr><td>Outcome</td><td><ul><li>A clear understanding of the requirements and desired outcome.</li><li>An overview of the structure of your product.</li><li>A specification ready to be handed over to your product designer for continuing on the detailed specification.</li></ul></td><td><ul><li>Deciding on the look and feel of your product.</li><li>A fully specified solution that can be handed to your technical team to start the service linking.</li></ul></td></tr><tr><td>How</td><td><a data-mention href="../using-uniscale/specification/high-level-specification/">high-level-specification</a></td><td><a data-mention href="../using-uniscale/specification/detailed-specification.md">detailed-specification.md</a></td></tr></tbody></table>



{% hint style="success" %}
**Validation**: We highly recommend validating both your high-level and detailed specifications with the relevant stakeholders to ensure complete alignment on the solution's purpose, objectives, and proposed UI and UX.&#x20;

This collaborative validation process ensures everyone understands the solution and its underlying rationale.
{% endhint %}



***

### Service linking

Here you will begin defining the architecture envisioned for your services, establishing their boundaries, and detailing how they will interact.&#x20;

<table><thead><tr><th width="127"></th><th width="601"></th></tr></thead><tbody><tr><td>What</td><td><p>Define the requirements for all technical functionality needed to build the intended user experience.</p><ul><li>Identify what functionality you would need from services to be able to implement this user experience</li><li>Define the initial architecture for your services.</li><li>Define your services' boundaries.</li><li>Outline how the services will interact with one another.</li></ul></td></tr><tr><td>Why</td><td>Ensure a sustainable product architecture with low technical debt and an optimized services dependency for better ownership distribution.</td></tr><tr><td>Who</td><td>Software architect or Tech Lead</td></tr><tr><td>Outcome</td><td>Having each UX flow linked to a service draft that is ready to be further described and modeled.</td></tr><tr><td>How</td><td><a data-mention href="../using-uniscale/documentation/service-linking/">service-linking</a></td></tr></tbody></table>



***

### Documentation

This is where you begin to model your services and outline the needed requirements to specify the technical functionality of your solution.

<table><thead><tr><th width="122"></th><th>High-level - Abstract</th><th>Detailed - Concrete</th></tr></thead><tbody><tr><td>What</td><td><p>Defining the requirements for technical functionality.</p><ul><li>Service functionality requirements</li><li>Definition of each service and its purpose</li></ul></td><td><p>Model how each service will work</p><ul><li>Endpoint modeling</li><li>Error code &#x26; sample data</li><li>Data validations</li></ul></td></tr><tr><td>Why</td><td>Describe and validate the purpose of each service to ensure a clean architecture.</td><td>Have a detailed overview of how each service is modeled and how they relate to each other.</td></tr><tr><td>Who</td><td>Software architect or Tech Lead</td><td>Software architect, Tech Lead, Software Engineer, or DevOps</td></tr><tr><td>Outcome</td><td>A clear overview of your services and understanding of their purpose.</td><td>Fully modeled services that are ready to be implemented.</td></tr><tr><td>How</td><td><a data-mention href="../using-uniscale/documentation/service-basics/">service-basics</a></td><td><a data-mention href="../using-uniscale/documentation/service-basics/">service-basics</a></td></tr></tbody></table>



***

### SDK Library

Here you will automatically generate and have access to an SDK library with a set of code snippets based on the documentation you have defined for your solution and services.

<table><thead><tr><th width="130"></th><th></th></tr></thead><tbody><tr><td>What</td><td>Collection of tools, code samples, and documentation that will be used by developers to build your solution.</td></tr><tr><td>Why</td><td>Allows for a decoupled backend and frontend and helps your developers to write better code.</td></tr><tr><td>Who</td><td>Software Developer</td></tr><tr><td>Outcome</td><td>Fully generated SDK library in the language of your choice.</td></tr><tr><td>How</td><td><a data-mention href="../using-uniscale/implementation/sdk-basics/#generating-the-sdk">#generating-the-sdk</a></td></tr></tbody></table>



{% hint style="success" %}
**Validation:** Ensure alignment with relevant stakeholders to confirm consensus on the generated SDK Library. This step is crucial to guarantee accurate implementation.
{% endhint %}



***

### Implementation

Here, you will write and implement your code in the Code Editor, utilizing our IDE plugin to enhance your coding efficiency and quality.

<table><thead><tr><th width="131"></th><th></th></tr></thead><tbody><tr><td>What</td><td>Involves writing and integrating code based on the specified functional and technical requirements defined inside Uniscale.</td></tr><tr><td>Why</td><td>Provides a seamless coding experience due to the IDE plugin.</td></tr><tr><td>Who</td><td>Software Developer</td></tr><tr><td>Outcome</td><td>Implement the required code to build your solution according to the functional and technical specifications within Uniscale.</td></tr><tr><td>How</td><td><a data-mention href="../using-uniscale/implementation/library-implementation-basics/">library-implementation-basics</a></td></tr></tbody></table>



In conclusion, the Uniscale Method stands out as a robust framework for collaborative software development, integrating domain-driven AI to streamline problem validation and optimize cost-effective solutions.&#x20;

By adhering to this structured approach, development teams can enhance their productivity, ensure alignment with project goals, and deliver high-quality software efficiently.&#x20;

Embracing the Uniscale Method not only fosters better collaboration but also paves the way for innovative and scalable software solutions



