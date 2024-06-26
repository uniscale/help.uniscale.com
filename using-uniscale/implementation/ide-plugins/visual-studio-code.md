# Visual Studio Code

### Installation

[Download the extension from VS Code from marketplace](https://marketplace.visualstudio.com/items?itemName=Uniscale.uniscale-develop) or search it from the extensions in the IDE itself:

<div align="left">

<figure><img src="../../../.gitbook/assets/Screenshot 2024-06-05 at 12.23.35.png" alt="" width="375"><figcaption><p>VS Code marketplace</p></figcaption></figure>

</div>

After installing the extension you will be prompted to login to Uniscale. Click "Login" to proceed:

<div align="left">

<figure><img src="../../../.gitbook/assets/Screenshot 2024-06-05 at 12.35.44.png" alt="" width="375"><figcaption><p>A notification to login into Uniscale</p></figcaption></figure>

</div>

This will open a dialog that will redirect you to the login website. Click "Open" to proceed:

<div align="left">

<figure><img src="../../../.gitbook/assets/Screenshot 2024-06-05 at 12.37.39.png" alt="" width="310"><figcaption><p>External website notification</p></figcaption></figure>

</div>

You will get this screen after a successful login. You are now logged in and you can start using Uniscale Develop:

<div align="left">

<figure><img src="../../../.gitbook/assets/Screenshot 2024-06-05 at 12.42.18.png" alt="" width="375"><figcaption><p>Succesful login</p></figcaption></figure>

</div>

All commands are prefixed with "Uniscale develop" so you can see all available commands by typing that into the command palette (⇧ + (⌘/ctrl) + P):

<figure><img src="../../../.gitbook/assets/Screenshot 2024-06-05 at 12.38.12.png" alt=""><figcaption><p>Command palette</p></figcaption></figure>

The description for all the available generative commands can be found from the [main page for IDE plugins.](./)

If you don't have any SDKs installed at this point you will see this prompt:

<div align="left">

<figure><img src="../../../.gitbook/assets/Screenshot 2024-06-05 at 12.53.50.png" alt="" width="375"><figcaption><p>Your project doesn't have any SDK installed</p></figcaption></figure>

</div>

This can be resolved by installing an SDK. The [Uniscale SDK portal ](../sdk-portal-overview.md)will provide you with instructions for your target language.



### VS Code commands

You can access all the available commands via the command palette (⇧ + (⌘/ctrl) + P).

`Uniscale Develop: Login to Uniscale`

Use this command to log into Uniscale. This command will be called automatically if you are not logged in and you call for snippet generation options.

`Uniscale Develop: SDK picker`

If you have multiple SDKs installed you can use this command to select the one that you want to use to generate snippets against.

`Uniscale Develop: Snippets and generative code`

This is the main command to retrieve a list of available generative commands. You might not see all the commands described here depending on what you have modeled in your solution and/or services. The full list can be seen in the section [Commands](./#commands) on the main page for more details.



### Troubleshooting

#### **I don't see snippets for things I just modeled**

You will need to generate a new SDK in Uniscale and install the new version as a dependency in your project.

#### **I see options for a wrong service**

You probably have more than one SDK installed simultaneously, you can see all installed SDKs and choose the one you want to use by issuing the command `Uniscale Develop: SDK picker`

#### **I don't see any options to generate snippets**

If you are not getting any snippet options or you get "fetch failed" errors you can try to log in again by issuing the command `Uniscale Develop: Login to Uniscale`. You can also try restarting VS Code.

#### **I got the "User is not part of the company" error**

This means that your user is not part of the company and/or the solution/service you are trying to access. Ask your administrator to add you to relevant solutions and services.



