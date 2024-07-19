---
description: Tenancy in systems
---

# Tenancy

**Tenancy in Data Model**

Tenancy in data modelling ensures that data segmentation is strictly maintained so that users or organisations can share the same system while keeping their data distinct and secure. It involves structuring the data model to support multiple tenants by logically isolating their data. This is crucial for maintaining data privacy, preventing unauthorised access, and ensuring that each tenant’s data remains isolated, mitigating risks of data leakage.



**Tenancy in Uniscale**

At Uniscale we prioritise data distinction and isolation within both the modelling and generated SDK.

We support tenancy at the two levels below;

* Data modelling level
* Solution Level&#x20;



**Data Modelling Level**

Tenancy in a data model ensures data segregation where the active context is not to be part of the model. This approach allows multiple users or organisations to share the same modules and or services while keeping their data isolated and secure.

<figure><img src="../../../.gitbook/assets/Screenshot 2024-05-15 at 16.28.13.png" alt=""><figcaption></figcaption></figure>

The circled property in the image above makes the model incorrect because it is adding the current logged in user identifier as part of the properties which goes against data segregation, which is a fundamental requirement for maintaining tenancy. By failing to isolate each tenant’s data, this model poses significant risks of data leakage or unauthorised access between different users or organisations. Correct implementations should guarantee that each tenant's data remains isolated and secure, preventing any potential overlap or interference.



**Solution level**

Uniscale addresses the solution tenancy by providing a robust and scalable framework that ensures strict data segregation. This platform prevents the inclusion of active context properties. By doing so, Uniscale upholds the principle of tenancy by isolating each tenant's data securely. This prevents any unauthorized access or data leakage, ensuring that each user's or organisation's data remains exclusively accessible to them, and maintains overall system integrity.

