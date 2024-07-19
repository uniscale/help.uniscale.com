---
description: >-
  This section defines the different approaches to defining data contracts
  within Uniscale, their benefits and also highlights the benefits of flattening
  lists when dealing with graph data
---

# Data Contract Composition

### **Building Blocks of Data Modeling at Uniscale**

In the world of software development, data modeling is a fundamental aspect that underpins the structure and organization of information. Uniscale utilizes a distinct approach to data contracts, leveraging three primary compositions: value objects, aggregates, and property groups. This article delves into each composition, illustrating their roles and significance within the Uniscale ecosystem.

### Understanding Data Contracts

Before we dive into the compositions, let's clarify the concept of data contracts. A data contract is a formal agreement that defines the structure, content, and validation rules for data exchanged between different components of a system. These contracts ensure data consistency, integrity, and reliability across the entire application landscape. The main forms of data contracts when modeling at Uniscale are Aggregates and Value Objects. both contracts define a series of properties that constitute an entity or object. it is also important to note that these properties can also be value objects and or aggregates. for example, you could have an employee aggregate with a property for a supervisor who would take on the structure of the aggregate employee.



**Aggregates: Mirroring the Data Layer**

Aggregates are the cornerstone of data modeling. They encapsulate related data elements, often representing entities or tables within a database. These objects typically include unique identifiers (such as primary keys) and properties that define the characteristics of the entity. Aggregates are the foundation for creating a structured and meaningful representation of the data layer within a software system.

<div align="left">

<figure><img src="../../../.gitbook/assets/Screenshot 2024-05-15 at 15.24.44.png" alt=""><figcaption><p>Aggregate</p></figcaption></figure>

</div>



**Value Objects: Lightweight Data Carriers**

Value Objects are designed for agility and data transfer. They represent a collection of values that are treated as a whole. Unlike Aggregates, Value Objects lack a unique identity. They are often used to populate API resources, enabling the movement of data between different components or systems. When a Value Object reaches its destination, its values can be used to populate an Aggregate, thereby bridging the gap between data representation and storage.

<div align="left">

<figure><img src="../../../.gitbook/assets/Screenshot 2024-05-15 at 15.26.22.png" alt=""><figcaption></figcaption></figure>

</div>

### Uniscale's Data Contract Ecosystem

The combination of Aggregates, Value Objects, and Property Groups forms a robust ecosystem for managing data within Uniscale. Aggregates provide a reliable representation of the database schema, while Value Objects ensure efficient data transfer between components. Property Groups keep data organized and easily accessible, making the codebase easier to understand and maintain.

This cohesive approach offers numerous benefits:

**Improved Data Integrity**: Data contracts define clear expectations for the structure and types of data, reducing errors and inconsistencies.

**Enhanced Code Readability**: Well-structured data contracts and compositions lead to more organized and understandable code.

**Easier Maintenance**: Changes to data structures can be managed more effectively through well-defined contracts and property groups.

**Seamless Data Exchange**: Value Objects facilitate smooth data transfer between different parts of the system or external APIs.



### Handling Graph Data

Graph data, with its interconnected nodes and relationships, is invaluable for representing complex systems. However, when it comes to data contracts, particularly for APIs or data exchange formats, traditional nested structures can become unwieldy and inefficient. An alternative approach, modeling graph data as flat lists with parent references, offers a compelling solution.

**The Nested Data Conundrum**

Nested data structures often mirror the inherent hierarchy of graphs. A node might contain child nodes, which in turn contain their own children, and so on. While this approach seems intuitive, it can quickly lead to several challenges:

* **Complexity**: Deeply nested structures become difficult to navigate and parse, both for humans and machines.
* **Rigidity**: Adding or removing relationships often requires significant schema changes, hindering flexibility.
* **Inefficiency**: Querying or manipulating nested data often involves recursive operations, impacting performance.

Imagine representing a company's organizational structure using nested data. Each employee node might contain a list of their subordinates, who in turn have their own subordinates, leading to a deeply nested structure:

```
{
  "name": "CEO",
  "subordinates": [
    {
      "name": "Manager A",
      "subordinates": [
        { "name": "Employee X", "subordinates": [] },
        { "name": "Employee Y", "subordinates": [] }
      ]
    },
    {
      "name": "Manager B",
      "subordinates": [
        { "name": "Employee Z", "subordinates": [] }
      ]
    },
    {
      "name": "Manager C",
      "subordinates": [
        { "name": "Employee W", "subordinates": [] },
        { "name": "Employee V", "subordinates": [] }
      ]
    }
  ]
}

```

This nested format quickly becomes complex, difficult to traverse, and inflexible when changes occur.

**The Flat List Paradigm**

Modeling graph data as a flat list, where each item represents a node, and parent references link them together, offers a refreshing alternative:

* **Simplicity**: A flat list is inherently easier to understand and manipulate. Each node is a separate entity with a clear parent reference.
* **Flexibility**: Adding or removing relationships becomes a matter of updating references, rather than restructuring the entire schema.
* **Performance**: Flat structures lend themselves well to efficient querying and manipulation, as relationships can be traversed directly through references.

Using a similar example as that illustrated above, the same data graph would look something like this.

```
[
  { "name": "CEO", "parentId": null },
  { "name": "Manager A", "parentId": "CEO" },
  { "name": "Employee X", "parentId": "Manager A" },
  { "name": "Employee Y", "parentId": "Manager A" },
  { "name": "Manager B", "parentId": "CEO" },
  { "name": "Employee Z", "parentId": "Manager B" },
  { "name": "Manager C", "parentId": "CEO" },
  { "name": "Employee W", "parentId": "Manager C" },
  { "name": "Employee V", "parentId": "Manager C" }
]
```

Flattening graph data contracts provides a powerful strategy for simplifying complex relationships, enhancing flexibility, and improving performance. While it requires a shift in thinking, the benefits often outweigh the initial adjustment, making it a valuable tool in data modeling . Whether you're designing APIs, data exchange formats, or simply managing complex data structures, consider the power of flattening to streamline your work and unlock the true potential of your graph data whilst using Uniscale
