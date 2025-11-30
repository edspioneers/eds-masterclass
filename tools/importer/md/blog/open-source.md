# Deno's Other Open Source Projects

Deno’s codebase - and most of what we build around it - is open source under the permissive MIT license. Over the years, we’ve published dozens of supporting libraries and tools that solve common problems we’ve run into while building Deno. Here are a few we think others may find useful.

- [`rusty_v8`: Rust bindings to the V8 JavaScript engine](#rusty_v8)
- [`deno_core`: builds on `rusty_v8` to provide higher level functionality, like mapping JavaScript `Promises` to Rust `Futures`](#deno_core)
- [`rust-urlpattern`: implements `URLPattern` web API in Rust](#rust-urlpattern)
- [`import_map`: implements the import map spec in Rust](#import_map)
- [`eszip` and `eszip_viewer`: a binary file format for distributing an entire module graph of TypeScript files](#eszip-and-eszip_viewer)
- [`sui`: a library for embedding data executable files in a cross platform way](#sui)
- [`dnt`: Deno to npm package build tool](#dnt)
- [`wasmbuild`: Build tool to use Rust code in Deno and the browser](#wasmbuild)
- [`monch`: lightweight parser, similar to `nom`, focused on strings](#monch)
- [`deno_task_shell`: cross-platform shell for `deno task`.](#deno_task_shell)
- [`flaky_test`: atttribute macro for running a flaky test multiple times](#flaky_test)
- [`vnotify`: monitor millions of S3 objects without external dependencies](#vnotify)
- [What’s next](#whats-next)

## Rusty V8

**[Rusty V8](https://github.com/denoland/rusty_v8)** provides high-quality, zero-overhead Rust bindings to V8’s C++ API, and is the core of the Deno runtime. We made this library, which has undergone over 150 releases and downloaded more than 3 million times on crates.io, [stable and production ready last year](/blog/rusty-v8-stabilized). You can use Rusty V8 to build custom JavaScript runtimes, run WebAssembly modules, use the V8 Fast API, and much more.

Here’s an example of how you can embed JavaScript in a Rust program with `rusty_v8`:

```
fn main() {
  // Initialize V8.
  let platform = v8::new_default_platform(0, false).make_shared();
  v8::V8::initialize_platform(platform);
  v8::V8::initialize();

  // Create a new Isolate and make it the current one.
  let isolate = &mut v8::Isolate::new(v8::CreateParams::default());

  // Create a stack-allocated handle scope.
  let handle_scope = &mut v8::HandleScope::new(isolate);

  // Create a new context.
  let context = v8::Context::new(handle_scope, Default::default());

  // Enter the context for compiling and running the hello world script.
  let scope = &mut v8::ContextScope::new(handle_scope, context);

  // Create a string containing the JavaScript source code.
  let code = v8::String::new(scope, "'Hello' + ' World!'").unwrap();

  // Compile the source code.
  let script = v8::Script::compile(scope, code, None).unwrap();

  // Run the script to get the result.
  let result = script.run(scope).unwrap();

  // Convert the result to a string and print it.
  let result = result.to_string(scope).unwrap();
  println!("{}", result.to_rust_string_lossy(scope));
}
```

## deno\_core

The [`deno_core`](https://github.com/denoland/deno_core) crate, builds on Rusty V8. Where Rusty V8 is truly exposes V8’s C++ API as directly as possible in Rust, `deno_core` adds “ops” and an event loop. Practically it maps JavaScript Promises onto Rust Futures. The “ops” are marcos which allow users to define functions that cross the boundary between JavaScript and Rust as efficently as possible (using V8’s Fast API where possible).

We’ve written some [blog posts](/blog/roll-your-own-javascript-runtime) about how one can use `deno_core` to quickly roll your own JavaScript runtime.

Although `deno_core` adds a lot on top of Rusty V8, it still lacks many things from the main deno runtime - it has no concept of TypeScript, it has very few APIs - no `fetch()` - and certainly no built-in node modules.

## rust-urlpattern

[This crate](https://github.com/denoland/rust-urlpattern) implements the `URLPattern` web API in Rust, following the specification as closely as possible. We use this …

```
use urlpattern::UrlPattern;
use urlpattern::UrlPatternInput;
use urlpattern::UrlPatternInit;

use urlpattern::UrlPattern;
use urlpattern::UrlPatternInit;
use urlpattern::UrlPatternMatchInput;

fn main() {
  // Create the UrlPattern to match against.
  let init = UrlPatternInit {
    pathname: Some("/users/:id".to_owned()),
    ..Default::default()
  };
  let pattern = <UrlPattern>::parse(init).unwrap();

  // Match the pattern against a URL.
  let url = "https://example.com/users/123".parse().unwrap();
  let result = pattern.exec(UrlPatternMatchInput::Url(url)).unwrap().unwrap();
  assert_eq!(result.pathname.groups.get("id").unwrap(), "123");
}
```

## import\_map

[`import_map`](https://github.com/denoland/import_map) is a Rust crate implementing the WICG Import Maps specification. An import map is a JSON file that lets you control how module specifiers resolve to actual URLs in JavaScript and TypeScript. We use this library to parse and apply import maps.

You can use `import_map` to create and map custom specifiers like `"my-lib"` to a full URL:

```
use import_map::ImportMap;
use url::Url;

// Define a base URL for relative mappings.
let base_url = Url::parse("file:///project/").unwrap();
// Create a new import map with a simple mapping:
let mut import_map = ImportMap::new(base_url);
import_map.imports_mut().insert(
    "my-lib".to_string(),
    Url::parse("https://cdn.example.com/my-lib@1.0/mod.js").unwrap()
);

// Resolve a specifier using the import map.
let specifier = "my-lib";
let resolved_url = import_map.resolve(specifier, &base_url).unwrap();
println!("'{}' resolves to {}", specifier, resolved_url);
```

## eszip and eszip\_viewer

The [`eszip`](https://github.com/denoland/eszip) format lets you losslessly serialize an ECMAScript module graph into a single compact file, allowing efficient storage and transmission of code as a single package. This is useful for creating standalone archives of JavaScript or TypeScript projects, or caching module graphs. It also supports streaming, so large module bundles can be loaded efficiently.

```
# Bundle a Deno module (and its dependencies) into an eszip file:
$ cargo run --example eszip_builder https://deno.land/std/http/file_server.ts file_server.eszip

# Later, view the contents of that eszip archive:
$ cargo run --example eszip_viewer file_server.eszip

# You can even execute the bundle by loading it into a V8 runtime (using an eszip loader).
$ cargo run --example eszip_load file_server.eszip https://deno.land/std/http/file_server.ts
```

We use `eszip` for quickly loading JavaScript and TypeScript in Deno Deploy. We also have [`eszip_viewer`](https://github.com/denoland/eszip_viewer) to easily view `eszip` formats.

## sui

[`sui`](https://github.com/denoland/sui) is a Rust library (named after the Hindi word for “needle”) that lets you embed data into executable files (ELF on Linux, PE on Windows, Mach-O on macOS), which can be extracted later. This is useful for bundling assets or configuration inside a binary without external files. `sui` produces valid executables that can be code-signed on macOS and Windows. [We use `sui` in `deno compile`](/blog/deno-compile-executable-programs#how-deno-compile-works) to minimize binary size and for code signing.

## dnt

[`dnt`](https://github.com/denoland/dnt) (Deno to npm transform) is [a build tool that converts a Deno module into a format publishable to npm](/blog/publish-esm-cjs-module-dnt) by shimming Deno-specific globals, rewriting import statements, and outputting types and CommonJS versions. This allows module authors to easily publish hybrid npm modules for ESM and CommonJS.

Here’s an example of using `dnt` in a build script to package your ES module:

```
// scripts/build_npm.ts
import { build, emptyDir } from "jsr:@deno/dnt";

await emptyDir("./npm");  // clear output directory
await build({
  entryPoints: ["./mod.ts"],    // your Deno module entry
  outDir: "./npm",              // output directory for the npm package
  shims: {
    deno: true                 // shim the Deno namespace for Node
  },
  package: {
    name: "your-package",
    version: "0.1.0",
    description: "Your package description",
    license: "MIT",
    repository: {
      type: "git",
      url: "git+https://github.com/yourname/your-repo.git"
    }
    // ... other package.json fields as needed
  }
});

// After this script runs, the "./npm" folder contains a package.json, README, and the transpiled code ready to publish.
```

## wasmbuild

[This CLI](https://github.com/denoland/wasmbuild) [simplifies the process of building and using Rust code in Deno and the browser](/blog/wasmbuild). It generates glue code for calling into Rust crates via `wasm-bindgen`. The output can be easily consumed in Javascript via Wasm. This tool is great in situations where you might want to call a complex algorithm in Rust from JavaScript, or run Rust code that is more efficient than in JavaScript.

For a more full example, check out [`wasmbuild_example`](/blog/wasmbuild) .

## monch

[This rust crate](https://github.com/denoland/monch) is a light-weight parser combinator library inspired by [`nom`](https://crates.io/crates/nom). It was created to provide a more targeted library for parsing strings and added some combinators we found useful. In Deno, `monch` is used to parse the `deno task` command strings and other similar situations.

```
use monch::*;

fn parse_comma_separated(input: &str) -> ParseResult<'_, Vec<&'_ str>> {
  let word = map(take_while(|c| c != ','), |v| v.trim());
  let comma = ch(',');
  separated_list(word, comma)(input)
}

let parse = with_failure_handling(parse_comma_separated);
println!("{:?}", parse("apple, banana   ,pear  ")); // Ok(["apple","banana","pear"])
```

## deno\_task\_shell

[`deno_task_shell`](https://github.com/denoland/deno_task_shell) is a cross-platform shell implementation for parsing and executing scripts. We use this in `deno task`.

```
// parse
let list = deno_task_shell::parser::parse(&text)?;

// execute
let env_vars = std::env::vars_os().collect::<HashMap<_, _>>();
let cwd = std::env::current_dir()?;

let exit_code = deno_task_shell::execute(
  list,
  env_vars,
  cwd,
  Default::default(), // custom commands
).await;
```

## flaky\_test

[`flaky_test`](https://github.com/denoland/flaky_test) is a Rust attribute macro that helps manage flaky tests by running a test multiple times and only failing it if it fails every time. This is useful for tests that are known to be flaky (due to non deterministic issues like network or availability). By default, the macro runs the marked test three times. If at least one run passes, the overall test is considered passed.

```
use flaky_test::flaky_test;

#[flaky_test]
fn my_unstable_test() {
    // This test will be tried up to 3 times.
    let result = some_operation_that_sometimes_flakes();
    assert!(result.is_ok());
}
```

## vnotify

[`vnotify`](https://github.com/denoland/vnotify) (short for “vectorized notification”) is a Rust library for efficiently monitoring changes in Amazon S3 buckets that contain millions of objects. It achieves this without any external services using a clever hashing strategy: when an object in S3 is updated, `vnotify` writes a small notification file under a special prefix. Clients can quickly check a fixed set of these notifications to detect updates across the whole bucket with one or two S3 API calls. This is useful for caching or syncing scenarios where you want to know if any object in a huge bucket changed without scanning the entire bucket.

```
use aws_sdk_s3::Client;
use vnotify::{VnotifyCache, Config};
use bytes::Bytes;

// Set up the S3 client and vnotify configuration.
let s3_client = Client::new(&aws_config::load_from_env().await);
let config = Config::new("my-bucket-name".to_string(), "vnotify_prefix/".to_string());
let cache = VnotifyCache::new(s3_client, config);

// Signal an update (writer side) – for example, after modifying "path/to/object".
cache.put("path/to/object", Bytes::from_static(b"1")).await?;
// (The content '1' is arbitrary; the key's ETag changing is what signals a change.)

// Later, a reader can quickly check if *any* object changed by checking the special "_" key:
if cache.try_get("_").await?.is_some() {
    println!("Some object in the bucket changed, need to refresh cache.");
    // The client could then list "vnotify_prefix/" keys to find out which segment changed.
}
```

## What’s next

These open source projects not only power Deno, but also used across the broader developer ecosystem. We’ll continue to build tools that make development simpler and more secure, and hope you’ll explore and build something great with them.

> **🚨️ [There have been major updates to Deno Deploy!](/deploy) 🚨️**
>
> - [New `deno --tunnel` command to connect your local and Deno Deploy environments](https://x.com/deno_land/status/1976281146184040625)
> - [Database connections and data explorer right in the UI](https://docs.deno.com/deploy/reference/databases/)
> - [Connect to AWS and GCP via Cloud Connections](https://docs.deno.com/deploy/reference/cloud-connections/)
> - [Automatic and immediate observability and telemetry](https://docs.deno.com/deploy/reference/observability/)

+--------------------------------------------------------------------+
| Metadata                                                           |
+=============+======================================================+
| Title       | Deno's Other Open Source Projects \| Deno            |
+-------------+------------------------------------------------------+
| Description | Here’s a roundup of some of our popular open source  |
|             | libraries and how we use them in Deno.               |
+-------------+------------------------------------------------------+
| Image       | ![Deno's Other Open Source Projects \| Deno][image0] |
+-------------+------------------------------------------------------+
| Date        | October 16, 2025                                     |
+-------------+------------------------------------------------------+
| Author      | Andy Jiang                                           |
+-------------+------------------------------------------------------+
| Tags        | Engineering                                          |
+-------------+------------------------------------------------------+

[image0]: http://localhost:3001/blog/open-source/og.png
