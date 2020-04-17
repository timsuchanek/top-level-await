# Top-level await

This is an attempt to get the [new top-level await](https://github.com/microsoft/TypeScript/pull/35813) introduced in TypeScript 3.8 running.

It's not running yet.
What works: `tsc -d` -> it compiles correctly.

What doesn't work: `node dist/index.js`. The output file has an actual top-level await, which can't be processed by Node.js

What also doesn't work: `ts-node index.ts`. It gets the following error:

```
const x = await doSomething();
          ^^^^^

SyntaxError: await is only valid in async function
    at wrapSafe (internal/modules/cjs/loader.js:1039:16)
    at Module._compile (internal/modules/cjs/loader.js:1087:27)
    at Module.m._compile (/Users/tim/code/repros/top-level-await/node_modules/ts-node/src/index.ts:836:23)
    at Module._extensions..js (internal/modules/cjs/loader.js:1143:10)
    at Object.require.extensions.<computed> [as .ts] (/Users/tim/code/repros/top-level-await/node_modules/ts-node/src/index.ts:839:12)
    at Module.load (internal/modules/cjs/loader.js:972:32)
    at Function.Module._load (internal/modules/cjs/loader.js:872:14)
    at Function.executeUserEntryPoint [as runMain] (internal/modules/run_main.js:71:12)
    at main (/Users/tim/code/repros/top-level-await/node_modules/ts-node/src/bin.ts:226:14)
    at Object.<anonymous> (/Users/tim/code/repros/top-level-await/node_modules/ts-node/src/bin.ts:485:3)
```
