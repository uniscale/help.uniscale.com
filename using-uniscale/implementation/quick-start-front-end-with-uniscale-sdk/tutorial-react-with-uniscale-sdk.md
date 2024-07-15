---
description: >-
  Welcome! In this tutorial we will build a simple react app using the Uniscale
  SDK.
---

# Tutorial: React with Uniscale SDK

### Step 1: Create a React app and install the SDK

Start a new React project using your preferred method. In this tutorial, we are using React + Next.js with TypeScript, but since we are only building a simple one-page app with very little functionality, the framework itself doesn't matter.

Run the following command and choose all default options:

```
npx create-next-app@latest
```

To use the SDK with our tutorial application, we will add an `.npmrc` file to the root of our project folder. The tutorial uses Uniscale Demo solution's SDK. Copy and paste the following block inside the `.npmrc` file you created:

```
@uniscale-sdk:registry=https://sdk.uniscale.com/api/packages/8c68f0da-8a3c-45bb-abba-2b6d36aa6b3c/npm/
//sdk.uniscale.com/api/packages/8c68f0da-8a3c-45bb-abba-2b6d36aa6b3c/npm/:_authToken=eb8a29eb2b95553972f408b1feb7dedeec016106
```

Now that you have configured the registry, you can install the SDK:

```
npm i @uniscale-sdk/ActorCharacter-Messagethreads@1.0.10
```

Now you have a folder structure like this:

```
app
  layout.tsx
  page.tsx
  ...etc
.npmrc
.package.json
...etc
```

### Step 2: Implement the platform dispatcher

Create a `dispatcher.ts` file inside your `app` folder. We will only use sample data from the SDK in this tutorial, so we will add a dispatcher and intercept only the features we want to use. Copy and paste this code block into the `dispatcher.ts` file you created:

```typescript
import {
  DispatcherSession,
  Platform,
} from "@uniscale-sdk/ActorCharacter-Messagethreads";
import { Patterns } from "@uniscale-sdk/ActorCharacter-Messagethreads/sdk/UniscaleDemo/Messages";
import { DirectMessageFull } from "@uniscale-sdk/ActorCharacter-Messagethreads/sdk/UniscaleDemo/Messages/Messages/DirectMessageFull";

export const initializeDispatcher = async (): Promise<DispatcherSession> => {
  const session = await Platform.builder()
    .withInterceptors((i) => {
      i.interceptRequest(
        Patterns.messages.getDirectMessageList.allRequestUsages,
        Patterns.messages.getDirectMessageList.handleDirect((_input, _ctx) => {
          return [DirectMessageFull.samples().defaultSample()];
        }),
      );
    })
    .build();

  return session
    .asSolution("fb344616-794e-4bd7-b81a-fb1e3361701f")
    .withLocale("en-GB")
    .withDataTenant("Customer 1 data tenant");
};
```

This function will return a `DispatcherSession` which we can later use to call any features specified in the SDK. See [#step-2-add-interceptors](./#step-2-add-interceptors "mention") from the Quick start tutorial on how to use interceptors to call real services. In a real-life scenario, you would replace the solution's UUID with your own solution's UUID. See more information here: [.](./ "mention")

Now your folder structure looks like this:

<pre><code>app
<strong>  <a data-footnote-ref href="#user-content-fn-1">dispatcher</a>.ts
</strong>  layout.tsx
  page.tsx
  ...etc
.npmrc
.package.json
...etc
</code></pre>

### Step 3: Initialize the dispatcher

It is recommended that you initialize the dispatcher only once when starting up your app. For the purpose of this tutorial, we will initialize the dispatcher inside our one-page application's top component, which is the `Home` component inside `page.tsx`. After successful initialization, we give the session to our app context, which will then allow any component within that context to use it.&#x20;

If you are using Next.js in a real-life scenario, you may want to handle the session builder very differently, but for the sake of a general solution that works with a basic react app, we are initializing the session here. The dispatcher could also be implemented in a singleton class.

Replace the content of your `page.tsx` with the following code block:

```typescript
"use client";
import { MessageList } from "./messages";
import { initializeDispatcher } from "./dispatcher";
import { useEffect, useState } from "react";
import { DispatcherSession } from "@uniscale-sdk/ActorCharacter-Messagethreads";
import { AppContextProvider } from "./app.context";

export default function Home() {
  const [dispatcherSession, setDispatcherSession] = useState<DispatcherSession>();

  useEffect(() => {
    const initialize = async () => {
      const session = await initializeDispatcher();
      setDispatcherSession(session);
    };

    initialize();
  }, []);

  if (!dispatcherSession) {
    return null;
  }

  return (
    <AppContextProvider dispatcherSession={dispatcherSession}>
      <main className="flex min-h-screen flex-col items-center justify-between p-24">
        <div />
      </main>
    </AppContextProvider>
  );
}
```

After adding the previous block, you should be getting errors from the missing `AppContextProvider`. Create a file `app.context.tsx` and copy and paste this code block inside it:

```typescript
import { DispatcherSession } from "@uniscale-sdk/ActorCharacter-Messagethreads";
import { FC, createContext, useContext, useState } from "react";

interface AppState {
  dispatcherSession: DispatcherSession;
  setState: React.Dispatch<React.SetStateAction<AppState>>;
}

const defaultAppState: AppState = {
  dispatcherSession: null as unknown as DispatcherSession,
  setState: (_value) => {
    throw new Error("App context not initialized");
  },
};

export const AppContext = createContext<AppState>(defaultAppState);

export const useAppContext = () => {
  return useContext(AppContext);
};

export const AppContextProvider: FC<{
  children: React.ReactNode;
  dispatcherSession: DispatcherSession;
}> = ({ children, dispatcherSession }) => {
  const [state, setState] = useState<AppState>({
    ...defaultAppState,
    dispatcherSession,
  });

  return (
    <AppContext.Provider value={{ ...state, setState }}>
      {children}
    </AppContext.Provider>
  );
};
```

Your folder structure will now look like this:

<pre><code>app
<strong>  app.context.tsx
</strong>  dispatcher.ts
  layout.tsx
  page.tsx
  ...etc
.npmrc
.package.json
...etc
</code></pre>

### Step 4: Use the dispatcher session in a component

Now that we have initialized the dispatcher and have a session stored in the app context, we can use the session to make requests. Create a new file `messages.tsx` and paste the following code block inside it:

```typescript
"use client";
import { useEffect, useState } from "react";
import { DirectMessageFull } from "@uniscale-sdk/ActorCharacter-Messagethreads/sdk/UniscaleDemo/Messages/Messages/DirectMessageFull";
import { GetDirectMessageList } from "@uniscale-sdk/ActorCharacter-Messagethreads/sdk/UniscaleDemo/Messages_1_0/Functionality/ServiceToModule/Messages/DirectMessages/ListDirectMessages/GetDirectMessageList";
import { useAppContext } from "./app.context";

export const MessageList = () => {
  const { dispatcherSession } = useAppContext();
  const [messages, setMessages] = useState<DirectMessageFull[]>([]);

  useEffect(() => {
    const getMessages = async () => {
      const directMessages =
        (await dispatcherSession.request(GetDirectMessageList.with()))?.value ||
        [];
      setMessages(directMessages);
    };

    getMessages();
  }, [dispatcherSession]);

  return (
    <div>
      {messages.map((m) => (
        <div key={m.directMessageIdentifier}>
          <p>{m.created?.at?.toString()}</p>
          <p>{m.message}</p>
        </div>
      ))}
    </div>
  );
};
```

This component will get any direct messages returned by the `GetDirectMessageList` endpoint. In this case, it only returns the sample data from the SDK, but in a real-life scenario, the session would make a `POST` request to a service.

Now replace the empty `<div />` inside page.tsx with `<MessageList />`

### Step 5: Run the app

Run the app with `npm run dev` or any script that works for your chosen environment.

You will now get a page with this text in the middle:

```
2020-02-28T08:09:10Z

Hello all
```

This is sample data returned from the session dispatcher. If you want to call a real API, you can modify `dispatcher.ts` to look like this:

```typescript
import {
  DispatcherSession,
  GatewayRequest,
  Platform,
  Result,
} from "@uniscale-sdk/ActorCharacter-Messagethreads";
import { Patterns } from "@uniscale-sdk/ActorCharacter-Messagethreads/sdk/UniscaleDemo/Messages";
import { DirectMessageFull } from "@uniscale-sdk/ActorCharacter-Messagethreads/sdk/UniscaleDemo/Messages/Messages/DirectMessageFull";

export const initializeDispatcher = async (): Promise<DispatcherSession> => {
  const session = await Platform.builder()
    .withInterceptors((i) => {
      // Sample data if GetDirectMessageList endpoint called
      i.interceptRequest(
        Patterns.messages.getDirectMessageList.allRequestUsages,
        Patterns.messages.getDirectMessageList.handleDirect((_input, _ctx) => {
          return [DirectMessageFull.samples().defaultSample()];
        }),
      );
      // Real api if any other Messages service endpoints called
      i.interceptPattern(Patterns.pattern, async (input, ctx) => {
        const headers = { "Content-Type": "application/json" };
        const response = await fetch(
          `/api/service-to-module/` + ctx.featureId,
          {
            method: "POST",
            headers,
            body: GatewayRequest.from(input, ctx).toJson(),
          },
        );
        return Result.fromJson(await response.json());
      });
    })
    .build();

  return session
    .asSolution("fb344616-794e-4bd7-b81a-fb1e3361701f")
    .withLocale("en-GB")
    .withDataTenant("Customer 1 data tenant");
};
```

At the end of this tutorial, your folder structure should look like this:

<pre><code>app
  app.context.tsx
  dispatcher.ts
  layout.tsx
<strong>  messages.tsx
</strong>  page.tsx
  ...etc
.npmrc
.package.json
...etc
</code></pre>

[^1]: 
