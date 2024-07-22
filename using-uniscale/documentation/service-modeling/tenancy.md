---
description: Tenancy in systems
---

# Tenancy

## **Tenancy in Data Model**

Tenancy in data modeling ensures that data segmentation is strictly maintained so that users or organizations can share the same system while keeping their data distinct and secure. It involves structuring the data model to support multiple tenants by logically isolating their data. This is crucial for maintaining data privacy, preventing unauthorized access, and ensuring that each tenant’s data remains isolated, mitigating risks of data leakage.



## **Tenancy in Uniscale**

At Uniscale we prioritise data distinction and isolation within both the modelling and generated SDK.

We support tenancy at the two levels below;

* [#data-modelling-level](tenancy.md#data-modelling-level "mention")
* [#solution-level](tenancy.md#solution-level "mention")



## **Data Modelling Level**

Tenancy in a data model ensures data segregation where the active context is not to be part of the model. This approach allows multiple users or organizations to share the same modules and or services while keeping their data isolated and secure.

<figure><img src="../../../.gitbook/assets/Screenshot 2024-05-15 at 16.28.13.png" alt=""><figcaption></figcaption></figure>

The circled property in the image above makes the model incorrect because it is adding the current logged-in user identifier as part of the properties which goes against data segregation, which is a fundamental requirement for maintaining tenancy. By failing to isolate each tenant’s data, this model poses significant risks of data leakage or unauthorized access between different users or organizations. Correct implementations should guarantee that each tenant's data remains isolated and secure, preventing any potential overlap or interference.



## **Solution level**

Uniscale addresses the solution tenancy by providing a robust and scalable framework that ensures strict data segregation. This platform prevents the inclusion of active context properties. By doing so, Uniscale upholds the principle of tenancy by isolating each tenant's data securely. This prevents any unauthorized access or data leakage, ensuring that each user's or organization's data remains exclusively accessible to them, and maintains overall system integrity.

