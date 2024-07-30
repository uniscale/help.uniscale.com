---
description: Learn how to use our IDE plugins for JetBrain
---

# JetBrains IDEs

### Installation

[Download the extension from JetBrains marketplace](https://plugins.jetbrains.com/plugin/24665-uniscale-develop) or install the plugin from JetBrains extension manager in the selected IDE:

<div align="left">

<figure><img src="../../../.gitbook/assets/Screenshot 2024-06-25 at 12.18.20.png" alt=""><figcaption><p>JetBrains marketplace in IDEA</p></figcaption></figure>

</div>

After installation, you can see available commands under Tools > Uniscale

<div align="left">

<figure><img src="../../../.gitbook/assets/Screenshot 2024-06-25 at 12.26.09.png" alt=""><figcaption><p>Locating Uniscale menu</p></figcaption></figure>

</div>

Use Tools > Uniscale > Login to Uniscale to start the login process. You will be redirected to the login page in your browser. You will get this screen after a successful login. You are now logged in and you can start using Uniscale Develop:

<div align="left">

<figure><img src="../../../.gitbook/assets/image (9) (2).png" alt=""><figcaption><p>Successful login</p></figcaption></figure>

</div>

Commands are displayed in the "Snippets and generative code" window (⌥ + ⌘ + U | Alt + Ctrl + U). The description for all the available generative commands can be found on the main page for [.](./ "mention")

<div align="left">

<figure><img src="../../../.gitbook/assets/Screenshot 2024-06-25 at 13.01.18.png" alt=""><figcaption><p>Command popup window</p></figcaption></figure>

</div>

If you don't have any SDKs installed at this point you will see this prompt:

<div align="left">

<figure><img src="../../../.gitbook/assets/Screenshot 2024-06-25 at 13.10.47.png" alt=""><figcaption><p>Your project doesn't have any SDK installed</p></figcaption></figure>

</div>

This can be resolved by installing an SDK. The [sdk-portal-overview.md](../sdk-basics/sdk-portal-overview.md "mention") will provide you with instructions for your target language.

If you haven't logged in yet or your session cannot be refreshed anymore, you will see this prompt:

<div align="left">

<figure><img src="../../../.gitbook/assets/Screenshot 2024-06-25 at 13.43.33.png" alt="" width="375"><figcaption><p>You need to login again</p></figcaption></figure>

</div>

This can be resolved by going through the login process again.



### JetBrains commands

You can access all the available commands via Tools > Uniscale

`Login to Uniscale`

Use this command to log into Uniscale.

`SDK selector`

If you have multiple SDKs installed you can use this menu to select the one you want to use to generate snippets against. Hovering the menu will display which SDK(s) are found.

`Snippets and generative code`

This is the main command to retrieve a list of available generative commands. Depending on what you have modeled in your solution and/or services, you might not see all the commands described here. A full list can be seen in the section [Commands](./#commands) on the main page for more details.
