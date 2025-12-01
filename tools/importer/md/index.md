# Uncomplicate JavaScript

Deno is the open-source JavaScript runtime for the modern web.

[Docs](https://docs.deno.com/)

[GitHub](https://github.com/denoland/deno/)

![][image0]

![][image1]![][image1]

![][image2]![An illustration in the style of lo-fi anime showing a cute dinosaur coding on a laptop in a cozy room. The laptop has a Deno sticker on the lid, and there's a steamy mug of coffee beside it. In the background is a plant, on the sill of a window overlooking hills and trees. It's dusk outside, with some stars visible in the upper skies, and it is raining gently as clouds slowly float past. The interior is warmly lit by a single desk lamp. On the desk is a takeout box, with chopsticks and a lemon beside it. Peeking over the edge of the box, barely visible, is DeeDee, the Deno Deploy mascot. Ferris, the Rust mascot, can also just barely be seen peeking out from inside the plant pot.][image3]

## Install Deno 2.5.6

[Release notes](https://github.com/denoland/deno/blob/main/Releases.md)

MacOS/Linux(Currently selected)

Windows

```
curl -fsSL https://deno.land/install.sh | sh
Copy command
```

![][image4]

## Deno is the open-source JavaScript runtime for the modern web.

Built on web standards with zero-config TypeScript, unmatched security, and a complete built-in toolchain.

- Rating

  100k+

  Stars on GitHub

- Community

  400k+

  Active Deno users

- Ecosystem

  2M+

  Community modules

* [![Slack][image5]](https://slack.com)
* [![Netlify][image6]](https://netlify.com)
* [![GitHub][image7]](https://github.com)
* [![Supabase][image8]](https://supabase.com)
* [![Salesforce][image9]](https://salesforce.com)
* [![Spotify][image10]](https://open.spotify.com/)
* [![Stripe][image11]](https://stripe.com)
* [![Bank of America][image12]](https://www.bankofamerica.com/)
* [![Tencent][image13]](https://tencent.com)

![][image14]

### Enterprise-grade JavaScript

Now offering enterprise support for the Deno runtime

[Learn more](/enterprise)

## All your favorite tools, built-in and ready to go

Deno natively supports TypeScript, JSX, and modern ECMAScript features with zero configuration.

![][image15]

account.ts

```
type User = { name: string; balance: number };

function getBalance(user: User): string {
  return `Balance: $${user.balance.toFixed(2)}`;
}

console.log(getBalance({ name: "Alice", balance: 42 }));
```

![][image15]

```
$ deno run account.ts
Balance: $42.00


$ deno check
Check account.ts
✅ Type check successful
```

### Just run

![TypeScript][image16]

Run `.ts` files directly with built-in type checking and compilation—no additional tooling or configuration required!

[More about TypeScript in Deno](https://docs.deno.com/runtime/fundamentals/typescript/)

### Seamless

With first-class support for npm and Node, Deno can read your `package.json` automatically, or you can import packages from npm directly.

[Node and npm support](https://docs.deno.com/runtime/manual/node)

![][image15]

Using package.json or import maps

```
import { Hono } from "hono";

const app = new Hono();

app.get("/", (c) => {
  return c.text("Hello Hono!");
});

Deno.serve(app.fetch);
```

![][image15]

Using inline imports

```
import { Hono } from "npm:hono@4";

const app = new Hono();

app.get("/", (c) => {
  return c.text("Hello Hono!");
});

Deno.serve(app.fetch);
```

## Built on web standards

Whenever possible, Deno implements web standard APIs on the server. Deno actively participates in [TC39](https://tc39.es/) and [WinterCG](https://wintercg.org/) to help move the web forward.

### Consistent code from browser to backend

Deno prioritizes web standard APIs, maximizing code reuse between browser and server and future-proofing your code.

[Web APIs in Deno](https://docs.deno.com/runtime/manual/runtime/web_platform_apis/)

![][image17]

[Skip past APIs list](#batteries-included)[Worker](https://developer.mozilla.org/docs/Web/API/Worker)[MessageEvent](https://developer.mozilla.org/docs/Web/API/MessageEvent)[WritableStreamDefaultController](https://developer.mozilla.org/docs/Web/API/WritableStreamDefaultController)[structuredClone](https://developer.mozilla.org/docs/Web/API/structuredClone)[DecompressionStream](https://developer.mozilla.org/docs/Web/API/DecompressionStream)[CompressionStream](https://developer.mozilla.org/docs/Web/API/CompressionStream)[setInterval](https://developer.mozilla.org/docs/Web/API/setInterval)[PromiseRejectionEvent](https://developer.mozilla.org/docs/Web/API/PromiseRejectionEvent)[clearInterval](https://developer.mozilla.org/docs/Web/API/clearInterval)[Blob](https://developer.mozilla.org/docs/Web/API/Blob)[fetch](https://developer.mozilla.org/docs/Web/API/fetch)[btoa](https://developer.mozilla.org/docs/Web/API/btoa)[localStorage](https://developer.mozilla.org/en-US/docs/Web/API/Window/localStorage)[Navigator](https://developer.mozilla.org/docs/Web/API/Navigator)[clearTimeout](https://developer.mozilla.org/docs/Web/API/clearTimeout)[ReadableStreamDefaultController](https://developer.mozilla.org/docs/Web/API/ReadableStreamDefaultController)[Response.json()](https://developer.mozilla.org/en-US/docs/Web/API/Response/json)[EventTarget](https://developer.mozilla.org/docs/Web/API/EventTarget)[caches](https://developer.mozilla.org/docs/Web/API/caches)[CacheStorage](https://developer.mozilla.org/docs/Web/API/CacheStorage)[MessagePort](https://developer.mozilla.org/docs/Web/API/MessagePort)[Location](https://developer.mozilla.org/docs/Web/API/Location)[DedicatedWorkerGlobalScope](https://developer.mozilla.org/docs/Web/API/DedicatedWorkerGlobalScope)[WebSocket](https://developer.mozilla.org/docs/Web/API/WebSocket)[queueMicrotask](https://developer.mozilla.org/docs/Web/API/queueMicrotask)[CryptoKey](https://developer.mozilla.org/docs/Web/API/CryptoKey)[ErrorEvent](https://developer.mozilla.org/docs/Web/API/ErrorEvent)[PerformanceMark](https://developer.mozilla.org/docs/Web/API/PerformanceMark)[WorkerNavigator](https://developer.mozilla.org/docs/Web/API/WorkerNavigator)[ReadableStreamBYOBRequest](https://developer.mozilla.org/docs/Web/API/ReadableStreamBYOBRequest)[TextDecoder](https://developer.mozilla.org/docs/Web/API/TextDecoder)[WorkerLocation](https://developer.mozilla.org/docs/Web/API/WorkerLocation)[TextEncoderStream](https://developer.mozilla.org/docs/Web/API/TextEncoderStream)[ReadableByteStreamController](https://developer.mozilla.org/docs/Web/API/ReadableByteStreamController)[TransformStream](https://developer.mozilla.org/docs/Web/API/TransformStream)[File](https://developer.mozilla.org/docs/Web/API/File)[CustomEvent](https://developer.mozilla.org/docs/Web/API/CustomEvent)[Event](https://developer.mozilla.org/docs/Web/API/Event)[performance](https://developer.mozilla.org/docs/Web/API/performance_property)[DOMException](https://developer.mozilla.org/docs/Web/API/DOMException)[ReadableStreamBYOBReader](https://developer.mozilla.org/docs/Web/API/ReadableStreamBYOBReader)[crypto](https://developer.mozilla.org/docs/Web/API/crypto_property)[CloseEvent](https://developer.mozilla.org/docs/Web/API/CloseEvent)[URLPattern](https://developer.mozilla.org/docs/Web/API/URLPattern)[PerformanceEntry](https://developer.mozilla.org/docs/Web/API/PerformanceEntry)[console](https://developer.mozilla.org/docs/Web/API/console)[globalThis.close()](https://developer.mozilla.org/en-US/docs/Web/API/Window/close)[Crypto](https://developer.mozilla.org/docs/Web/API/Crypto)[Request](https://developer.mozilla.org/docs/Web/API/Request)[ReadableStream](https://developer.mozilla.org/docs/Web/API/ReadableStream)[Storage](https://developer.mozilla.org/docs/Web/API/Storage)[WebAssembly](https://developer.mozilla.org/en-US/docs/WebAssembly)[TextDecoderStream](https://developer.mozilla.org/docs/Web/API/TextDecoderStream)[URLSearchParams](https://developer.mozilla.org/docs/Web/API/URLSearchParams)[ProgressEvent](https://developer.mozilla.org/docs/Web/API/ProgressEvent)[FileReader](https://developer.mozilla.org/docs/Web/API/FileReader)[ByteLengthQueuingStrategy](https://developer.mozilla.org/docs/Web/API/ByteLengthQueuingStrategy)[BeforeUnloadEvent](https://developer.mozilla.org/docs/Web/API/BeforeUnloadEvent)[TextEncoder](https://developer.mozilla.org/docs/Web/API/TextEncoder)[atob](https://developer.mozilla.org/docs/Web/API/atob)[globalThis.alert()](https://developer.mozilla.org/en-US/docs/Web/API/Window/alert)[setTimeout](https://developer.mozilla.org/docs/Web/API/setTimeout)[Performance](https://developer.mozilla.org/docs/Web/API/Performance)[Headers](https://developer.mozilla.org/docs/Web/API/Headers)[WorkerGlobalScope](https://developer.mozilla.org/docs/Web/API/WorkerGlobalScope)[AbortSignal](https://developer.mozilla.org/docs/Web/API/AbortSignal)[FormData](https://developer.mozilla.org/docs/Web/API/FormData)[Response](https://developer.mozilla.org/docs/Web/API/Response)[MessageChannel](https://developer.mozilla.org/docs/Web/API/MessageChannel)[URL](https://developer.mozilla.org/docs/Web/API/URL)[BroadcastChannel](https://developer.mozilla.org/docs/Web/API/BroadcastChannel)[TransformStreamDefaultController](https://developer.mozilla.org/docs/Web/API/TransformStreamDefaultController)[SubtleCrypto](https://developer.mozilla.org/docs/Web/API/SubtleCrypto)[Cache](https://developer.mozilla.org/docs/Web/API/Cache)[WritableStream](https://developer.mozilla.org/docs/Web/API/WritableStream)[AbortController](https://developer.mozilla.org/docs/Web/API/AbortController)[ReadableStreamDefaultReader](https://developer.mozilla.org/docs/Web/API/ReadableStreamDefaultReader)[PerformanceMeasure](https://developer.mozilla.org/docs/Web/API/PerformanceMeasure)[WritableStreamDefaultWriter](https://developer.mozilla.org/docs/Web/API/WritableStreamDefaultWriter)

## Batteries included

The essential tools you need to build, test, and deploy your applications are all included out of the box.

### Code linter

Deno ships with a built-in code linter to help you avoid bugs and code rot.

[Learn more ›](https://docs.deno.com/runtime/manual/tools/linter)

```
$ deno lint --watch
```

![][image18]

### Test runner

Deno provides a test runner and assertion libraries as a part of the runtime and standard library.

[Learn more ›](https://docs.deno.com/runtime/manual/basics/testing/)

```
// server_test.ts
Deno.test("1 + 2 = 3", () => {
  const x = 1 + 2;
  console.assert(x == 3);
});
```

```
$ deno test server_test.ts
```

### Standalone executables

Instantly create standalone executables from your Deno program. It even supports cross-compiling for other platforms!

[Learn more ›](https://docs.deno.com/runtime/manual/tools/compiler)

```
Deno.serve(req => new Response("Hello!"));
```

```
$ deno compile --allow-net server.ts

Compile file:///tmp/server.ts to server
$ ./server
Listening on http://localhost:8000/
```

### Code formatter

Deno's built-in code formatter (based on dprint) beautifies JavaScript, TypeScript, JSON, and Markdown.

[Learn more ›](https://docs.deno.com/runtime/manual/tools/formatter)

```
$ deno fmt --line-width=120
```

![][image19]

## Secure by default

A program run with Deno has no file, network, or environment access unless explicitly enabled.

### Prevent supply chain attacks

Stop worrying about npm modules introducing unexpected vulnerabilities. Deno restricts access to the file system, network, and system environment by default, so code can access only what you allow.

[Security in Deno](https://docs.deno.com/runtime/manual/basics/permissions)

#### Other runtimes

```
$ node random.js
Executing random.js...
🚨 File system compromised!
```

#### Deno

```
$ deno random.js
⚠️ Deno requests write access
Allow? [y/n/A]
$ n
❌ Denied write access
Exited
```

### High-performance networking

Out of the box support for:

- HTTPS (encryption)
- WebSocket
- HTTP2
- Automatic response body compression

[View documentation](https://docs.deno.com/runtime/manual/runtime/http_server_apis/)

#### Requests per second\*

More is better

Deno

0

Node

0

\* Ubuntu 22 on ec2 m5.metal; Deno 2.5.2 vs. Node 18.12.1

## Built for the cloud

Whether you deploy with our lightning-fast Deno Deploy or on other cloud providers, Deno streamlines your experience.

### — Deno runs on —

- [Official Docker image](https://hub.docker.com/r/denoland/deno "Docker")
- [hayd/deno-lambda](https://github.com/hayd/deno-lambda "AWS Lambda distribution")
- [How to Deploy Deno to Digital Ocean](https://docs.deno.com/runtime/manual/advanced/deploying_deno/digital_ocean "DigitalOcean")
- [Run a Deno App - Fly.io Docs](https://fly.io/docs/languages-and-frameworks/deno/ "Fly.io")
- [skymethod/denoflare](https://github.com/skymethod/denoflare "Cloudflare")
- [anthonychu/azure-functions-deno-worker](https://github.com/anthonychu/azure-functions-deno-worker "Azure")
- [How to Deploy to Google Cloud Run](https://docs.deno.com/runtime/manual/advanced/deploying_deno/google_cloud_run "Google Cloud Run")

## — The cloud built for modern JavaScript —

### Project hosting made for Deno

Unlock the full potential of your JavaScript and TypeScript projects with the all-new, completely reimagined Deno Deploy

[![][image20]](/video/playground-1-720.mp4?__frsh_c=0a3729d6bcaef11865d40ac9cc0bcd828a21dbd4)

### Unlock the full power of Deno

Deno users can enjoy first-class support for features like OpenTelemetry, Deno KV, and the Deno Deploy CLI—plus exclusives like Playgrounds, Databases, and more.

### Built for anything built with JavaScript

Because Deno is compatible with Node, your teams and projects can enjoy Deno Deploy's powerful features—even if you're not using Deno

- [Fresh logo](https://fresh.deno.dev/ "Fresh")
- [Vue logo](https://vuejs.org/ "Vue")
- [Hono logo](https://hono.dev/ "Hono")
- [Next logo](https://nextjs.org/ "Next")

* [Solid Start logo](https://start.solidjs.com/ "Solid Start")
* [Nuxt logo](https://nuxt.com/ "Nuxt")
* [SvelteKit logo](https://kit.svelte.dev/ "SvelteKit")
* [Docusaurus logo](https://docusaurus.io/ "Docusaurus")

- [React logo](https://reactjs.org/ "React")
- [Astro logo](https://astro.build/ "Astro")
- [Solid logo](https://www.solidjs.com/ "Solid")
- [Remix logo](https://remix.run/ "Remix")

* [Vite logo](https://vite.dev/ "Vite")
* [Express logo](https://expressjs.com/ "Express")
* [Deno logo](/ "Deno")
* [Node logo](https://nodejs.org/ "Node")

[Learn more about Deno Deploy](/deploy)

[Pricing](/pricing)[Sign in](https://console.deno.com)

![][image21]

## Get the most out of Deno with Fresh 2.0

[Fresh](https://fresh.deno.dev) is the Deno web framework, built with [Preact](https://preactjs.com/) and fully compatible with [Vite](https://vitejs.dev/) for blazing speed and instant productivity.

### Build fast sites fast

Author routes as the JSX (or TSX) components you already know and love, and Fresh handles dynamic server-side rendering by default.

![][image15]

/routes/index.tsx

```
export default function HomePage() {
  return (
    <div>
      <h1>HTML fresh from the server!</h1>
      <p>
        Delivered at
        {new Date().toLocaleTimeString()}
      </p>
    </div>
  );
}
```

![][image15]

/islands/Counter.tsx

```
import { useSignal } from "@preact/signals";

export default function Counter() {
  const count = useSignal<number>(0);

  return (
    <button onClick={() => count.value += 1}>
      The count is {count.value}
    </button>
  );
}
```

### Ship less JavaScript

Island-based architecture lets you opt in to only the JavaScript you need, for absolutely minimal runtime overhead.

[Learn more about Fresh](https://fresh.deno.dev/)

Our vibrant community

> “I knew this was gonna happen! Deno is truly building the fastest, most secure and personalizable JS runtime!”

Manu (Qwik)

> “Deno's security model is PERFECT for this type of script. Running a script from a rando off the internet? It asks for read access to only the CWD and then asks for access to the file it wants to write to. 👏”

Wes Bos

> “I really think Deno is the easiest and most capable JS runtime. URL imports are slept on.”

Atalocke

> “npm packages in Deno 👀 That’s an exciting development for those of us building at the edge.”

Jason Lengstorf

> “This Deno thing is fast, no doubt about it. #denoland”

Poorly Funded Snob

> “Deno: I have to use the browser APIs cause they are everywhere, and everywhere is my target runtime (the web). The runtime that tries to mirror browser APIs server side makes my life easiest.”

Taylor Young

> “Deno is fantastic. I am using it to level up a bit in terms of JavaScript and TypeScript and it is the easiest way to get going. Their tooling is like 100x simpler than all the usual Node stacks.”

Stefan Arentz

- Manu (Qwik)(active)
- Wes Bos
- Atalocke
- Jason Lengstorf
- Poorly Funded Snob
- Taylor Young
- Stefan Arentz

![][image14]

## Ready to get started with Deno?

[Install now](https://docs.deno.com/runtime/manual)

[Read the docs](https://docs.deno.com)

+------------------------------------------------------------------------------+
| Metadata                                                                     |
+=============+================================================================+
| Title       | Deno, the next-generation JavaScript runtime                   |
+-------------+----------------------------------------------------------------+
| Description | Deno features improved security, performance, and developer    |
|             | experience compared to its predecessor. It's a great time to   |
|             | upgrade your Node.js project to run on Deno.                   |
+-------------+----------------------------------------------------------------+
| Image       | ![A logo of a sauropod in the rain and the word Deno][image22] |
+-------------+----------------------------------------------------------------+

[image0]: http://localhost:3001/images/homepage/lofi-hero-bg.webp?__frsh_c=0a3729d6bcaef11865d40ac9cc0bcd828a21dbd4

[image1]: http://localhost:3001/images/homepage/lofi-hero-clouds.webp?__frsh_c=0a3729d6bcaef11865d40ac9cc0bcd828a21dbd4

[image2]: http://localhost:3001/images/homepage/lofi-hero-fg.webp?__frsh_c=0a3729d6bcaef11865d40ac9cc0bcd828a21dbd4

[image3]: http://localhost:3001/images/homepage/lofi-placeholder-rain.webp?__frsh_c=0a3729d6bcaef11865d40ac9cc0bcd828a21dbd4

[image4]: http://localhost:3001/images/homepage/peeking.svg?__frsh_c=0a3729d6bcaef11865d40ac9cc0bcd828a21dbd4

[image5]: http://localhost:3001/images/lp/companies/slack.svg?__frsh_c=0a3729d6bcaef11865d40ac9cc0bcd828a21dbd4

[image6]: http://localhost:3001/images/lp/companies/netlify.svg?__frsh_c=0a3729d6bcaef11865d40ac9cc0bcd828a21dbd4

[image7]: http://localhost:3001/images/lp/companies/github.svg?__frsh_c=0a3729d6bcaef11865d40ac9cc0bcd828a21dbd4

[image8]: http://localhost:3001/images/lp/companies/supabase.svg?__frsh_c=0a3729d6bcaef11865d40ac9cc0bcd828a21dbd4

[image9]: http://localhost:3001/images/lp/companies/salesforce.svg?__frsh_c=0a3729d6bcaef11865d40ac9cc0bcd828a21dbd4

[image10]: http://localhost:3001/images/lp/companies/spotify.svg?__frsh_c=0a3729d6bcaef11865d40ac9cc0bcd828a21dbd4

[image11]: http://localhost:3001/images/lp/companies/stripe.svg?__frsh_c=0a3729d6bcaef11865d40ac9cc0bcd828a21dbd4

[image12]: http://localhost:3001/images/lp/companies/bank-of-america.svg?__frsh_c=0a3729d6bcaef11865d40ac9cc0bcd828a21dbd4

[image13]: http://localhost:3001/images/lp/companies/tencent.svg?__frsh_c=0a3729d6bcaef11865d40ac9cc0bcd828a21dbd4

[image14]: http://localhost:3001/images/homepage/side-peek.svg?__frsh_c=0a3729d6bcaef11865d40ac9cc0bcd828a21dbd4

[image15]: http://localhost:3001/images/icons/window-buttons.svg?__frsh_c=0a3729d6bcaef11865d40ac9cc0bcd828a21dbd4

[image16]: http://localhost:3001/runtime/typescript.png?__frsh_c=0a3729d6bcaef11865d40ac9cc0bcd828a21dbd4

[image17]: http://localhost:3001/images/homepage/peek-around.svg?__frsh_c=0a3729d6bcaef11865d40ac9cc0bcd828a21dbd4

[image18]: http://localhost:3001/images/homepage/code_lines.svg?__frsh_c=0a3729d6bcaef11865d40ac9cc0bcd828a21dbd4

[image19]: http://localhost:3001/images/homepage/formatter_lines.svg?__frsh_c=0a3729d6bcaef11865d40ac9cc0bcd828a21dbd4

[image20]: /video/thumbnails/playground-1-720.jpg

[image21]: http://localhost:3001/runtime/fresh.svg?__frsh_c=0a3729d6bcaef11865d40ac9cc0bcd828a21dbd4

[image22]: http://localhost:3001/og/image.jpg
