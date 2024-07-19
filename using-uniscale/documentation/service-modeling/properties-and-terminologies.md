# Properties & Terminologies

## Properties & Terminologies

Understanding **properties** and **terminologies** is crucial for effective data categorization and operation within uniscale. This section delineates their differences, attributes, and application scenarios providing clarity on their usage.

### Properties

A **property** represents a data field that holds values defining characteristics of an object or entity within uniscale. In particular; **value objects**, **aggregates** and **property groups** can contain properties.

Value objects are defined [_**here**_](#user-content-fn-1)[^1] and aggregates are defined [_**here**_](#user-content-fn-2)[^2];

Property groups, as implied by their name, are collections of related properties bundled together. For example, while modeling an address, one might combine properties such as street address, city, and country into a single "address property group." This approach simplifies the organization of related properties.

**Types of Properties:**

We have 3 distinct types of properties; **native** properties, **reference** properties and **value object** properties  and each of these types can be sub-categorised as below

* **Native:**
  * `String`: Contains text.
  * `Boolean`: Represents `true` or `false`.
  * `Int`: An integer number.
  * `Float`: A number that includes a decimal point.
  * `Date`: Represents date only.
  * `DateTime`: Combines date and time.
  * `Guid`: Globally unique identifier.
  * `Terminology`: Enum-like structure housing predefined data points. (see further breakdown below)
* **References:** Point to other entities or objects.
* **Value Objects:**
  * **Create New (for company):** Generates a value object accessible company-wide.
  * **Create New (for product):** Generates a product-specific value object.
  * **Available Value Objects:** Selection from pre-existing value objects.

**Cardinality:**

* `Single`: Property can hold only one value.
* `Multiple`: Property can hold multiple values.



To create a property, you can start by creating a value object for example...

<figure><img src="../../../.gitbook/assets/Screenshot 2024-04-23 at 19.14.51.png" alt=""><figcaption><p>"Plot" as a property of value object StreetAddress</p></figcaption></figure>

After creating a property, selecting it will open a context menu on the right side where you can adjust its types and cardinalities as follows:...

<figure><img src="../../../.gitbook/assets/Screenshot 2024-04-23 at 19.15.03.png" alt=""><figcaption><p>select property type</p></figcaption></figure>

<figure><img src="../../../.gitbook/assets/Screenshot 2024-04-23 at 19.18.46.png" alt=""><figcaption><p>select a data type for the property</p></figcaption></figure>

### Terminologies

#### What is a Terminology:

A **terminology** is a subtype of native properties. It is akin to an enumeration (`enum`) in programming, offering a predefined set of data points. This structure enables controlled vocabulary within fields where only specified values are permitted, ensuring data integrity and consistency.

Given an example of a phone number, we can have a terminology property for "Type"...

<figure><img src="../../../.gitbook/assets/Screenshot 2024-04-23 at 20.49.19.png" alt=""><figcaption></figcaption></figure>

we can add two possible values for this terminology, "Home" and "Work" meaning when this property is used, it can only take on the values of either "work" or "home"

<figure><img src="../../../.gitbook/assets/Screenshot 2024-04-23 at 20.49.54.png" alt=""><figcaption></figcaption></figure>

[^1]: add link to documentation

[^2]: add link to documentation
