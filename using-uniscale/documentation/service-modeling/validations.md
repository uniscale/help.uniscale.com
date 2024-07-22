---
description: >-
  This page describes what Property validations are and how they can be set when
  creating properties.
---

# Validations

In the `Modeling view` under the `Technical view`, when adding properties, you can also specify validations for these properties.

<figure><img src="../../../.gitbook/assets/Screenshot 2024-04-23 at 14.54.21.png" alt=""><figcaption></figcaption></figure>

## Property Validations

Property validations are crucial for various native object types to ensure data integrity and compliance with business rules. The types of validations include:

* **Integer & Float**:
  * Ensure numeric values fall within accepted thresholds (e.g., non-negative quantities).
  * Confirm inputs expected to be numeric truly are.
* **String**:
  * Enforce length constraints (minimum or maximum characters).
  * Validate content against specific formats or regex patterns (e.g., email addresses).
  * Limit content to permissible characters.
* **Date & Datetime**:
  * Check values are within an acceptable logical range.
  * Ensure chronological order for a series of dates (start date comes before end date).
  * Verify correct formatting according to application standards.

To begin adding a validation, click the **property** of interest to access the sidebar, then navigate to the settings tab. It's important to note that only properties labeled with a Property Type **`Native type`** can have validations set. Once this is confirmed, select the _**data type**_ that matches one of the previously listed validation types. The process is detailed below.

<figure><img src="../../../.gitbook/assets/Screenshot 2024-04-23 at 15.05.42.png" alt="" width="185"><figcaption></figcaption></figure>



## Validation Tab

With the validation tab visible, under the field restrictions, we do see a couple of extra options listed below as:

* No validation
* Forced validation
* Validation options

<figure><img src="../../../.gitbook/assets/Screenshot 2024-04-23 at 15.22.58.png" alt="" width="373"><figcaption></figcaption></figure>

## No validation

The first option is as self-explanatory as we would expect. No validation would be applied to the property.&#x20;



### Forced validation

The second option _**Forced validation**_ displays a restriction option with the ability to add a restriction based on the type of validation selected**.**

<figure><img src="../../../.gitbook/assets/Screenshot 2024-04-23 at 15.38.34.png" alt="" width="370"><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/Screenshot 2024-04-23 at 15.41.48.png" alt="" width="375"><figcaption><p>This window is displayed when the add restriction button is clicked to add the "custom" validation.</p></figcaption></figure>

Once the changes have been saved, our validation is applied to the property going forward.&#x20;

The above example applies to the _**string**_ validation but the other validation types may defer on how they are presented when the **`Add+`** restriction button is clicked as shown below.&#x20;

<figure><img src="../../../.gitbook/assets/Screenshot 2024-04-23 at 15.45.42.png" alt=""><figcaption><p>Integer / Float validation shows option types Less than, Greater than or In between.</p></figcaption></figure>

<figure><img src="../../../.gitbook/assets/Screenshot 2024-04-23 at 16.21.29.png" alt=""><figcaption><p>Date validation shows type options as Before date, After date &#x26; Between dates. </p></figcaption></figure>

With regards to the date time validations,  we have extra options as seen below that are helpful if in need of more refined date time validation.&#x20;

<figure><img src="../../../.gitbook/assets/Screenshot 2024-05-15 at 11.53.57.png" alt=""><figcaption><p>Date time validation with interval type Fixed date window</p></figcaption></figure>

In the above screenshot, expanded options for date and time validation ensure inputs meet specific criteria. You can specify a date range, enforce a specific format, and apply conditional logic, such as checking if a date falls on a weekday. These features provide robust flexibility for precise data validation in forms or applications, ensuring data integrity and consistency.



<figure><img src="../../../.gitbook/assets/Screenshot 2024-05-15 at 11.55.18.png" alt=""><figcaption><p>Date time validation with interval type Floating date window</p></figcaption></figure>

The screenshot above offers an in-depth look at the advanced date and time validation options available within the platform. These options extend beyond simple date restrictions to provide a higher degree of control and specificity. Users can define date ranges to ensure inputs fall within a particular timeframe, enforce specific date and time formats to maintain consistency, and apply sophisticated conditional logic—such as requiring that a date be a weekday or excluding holidays. The floating date window does not have a specific or fixed day, week, month, or year with time in regards to the range selection.&#x20;



<figure><img src="../../../.gitbook/assets/Screenshot 2024-05-15 at 11.53.57 (1).png" alt=""><figcaption><p>Interval type Fixed date window with optional time window</p></figcaption></figure>

The screenshot above demonstrates the advanced date and time validation options available. Users can define specific date ranges, enforce particular date and time formats, and apply conditional logic such as ensuring a date falls on a weekday or excluding holidays. The floating date window feature allows for a flexible range selection without fixed days, weeks, months, or years.



### Validation options

The third and last option _**Validation options**_ adds a few extra options besides the Restriction option as seen in the second option. The extra options when selected are also applied to the property as seen below.&#x20;

<figure><img src="../../../.gitbook/assets/Screenshot 2024-04-23 at 15.55.20.png" alt="" width="371"><figcaption></figcaption></figure>

Overall, property validations across these native object types are fundamental to ensuring that data stored and processed by applications meet defined constraints and business rules. Adding these validations can significantly reduce errors, enhance data quality, and provide a better user experience.
