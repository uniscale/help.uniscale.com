# Namespace parameters

In the world of service design and modeling, namespace parameters can play a crucial role in organizing and managing data efficiently. This section will help you understand what namespace parameters are, their importance, and how to effectively use them in your projects.



## What Are Namespace Parameters?

Namespace parameters are defined variables that are applicable across multiple endpoints within a namespace hierarchy. They can serve as essential context carriers, ensuring that consistent data references are maintained throughout different parts of your service. Think of namespace parameters as shared properties that streamline communication between various components of your service architecture.

Namespace parameters are available as generic information when using the SDK. This means that you can work with namespace parameters in code even if you do not know the endpoint or its input and output contracts. This allows to implement for example generic data access control mechanisms and referential validation.

For instance, let's say we are designing a service that contains information about companies and we add a namespace for that called Companies. Under that namespace you might have endpoints for creating a company, changing a company's name, specifying an address, and more. Except for creating the company the remaining endpoints all require the company id. As such the company can be considered a namespace parameter of that namespace. Once it is defined as a namespace parameter it will be available for all endpoints in the namespace hierarchy.&#x20;



## Managing namespace parameters

To manage namespace parameters click on “manage namespace parameters” from the namespace action menu:

<figure><img src="../../../.gitbook/assets/CleanShot 2024-07-26 at 10.48.34@2x.png" alt=""><figcaption></figcaption></figure>

From the right side toolbar that is opened you can add, edit and delete namespace parameters:

<figure><img src="../../../.gitbook/assets/CleanShot 2024-07-26 at 10.50.57@2x.png" alt=""><figcaption></figcaption></figure>

When you add a new namespace parameter you need to specify the parameter type and name:

<figure><img src="../../../.gitbook/assets/CleanShot 2024-07-26 at 10.51.33@2x.png" alt=""><figcaption></figcaption></figure>

Once you have added namespace parameters you will see that next to the domain name there is a {/} icon indicating this namespace has parameters:

<figure><img src="../../../.gitbook/assets/CleanShot 2024-07-26 at 10.47.44@2x.png" alt=""><figcaption></figcaption></figure>



## Using namespace parameters

After you have added namespace parameters you can start taking them in to use in your endpoint definitions.&#x20;

To do this, just create an endpoint, enable namespace parameters, and configure which parameters you want to use in the endpoint:

<figure><img src="../../../.gitbook/assets/CleanShot 2024-07-26 at 10.58.51@2x.png" alt=""><figcaption></figcaption></figure>



## Using namespace parameters with the SDK

Once you have generated an SDK that contains features with namespace parameters you will notice that when you start to instantiate the feature it will in addition to the request body require the defined namespace parameters. For example in Java:

```java
UpdateCompanyName
    .with(UUID.fromString("<COMPANY_ID>"), 
        UpdateCompanyNameInput
            .builder()
            .name("New name")
            .build()
        );
```

On the receiving end, you can access the namespace parameters of the feature call by using the FeatureContext of the call:

```java
UUID companyId = ctx.getNamespaceParameter(NamespaceParameters.companyId);

```

The NamespaceParameters class contains all the defined namespace parameters and will help you to work with them.
