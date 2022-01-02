# Scratchpad

## Elements shouldn’t be built in to the system. Preact shouldn’t be built into the system???

On the server-side, there could be a plugin that enables the [[Elements]] API, including the registry, and the parsing of them. On the client side, there’s no reason that Preact has to be sent by the server, it could (again) be injected by the client. An [[Injection]] API should exist for that, although I’m unsure if it should be in the core or if it should be a member of a Views add-on plugin. On the Admin side, it gets a little weirder, since I use contexts to pass down state that would be hard to send down otherwise. I suppose the [[Editor]] as a whole should be a plugin, and if we’re abstracting elements into a plugin it could be dependent on that. Manual state copying could be used to pass stuff across Preact contexts, which would be a little dirty but who cares, it works.

## Routing shouldn’t be a built-in thing either.

Why is it, anyways? I could simply expose the Express’s [[Raw Routing]] mechanics to the API and allow a plugin to create the concept of Routes and Views.

## API Registry for APIs?

Maybe there shouldn’t be a global API object. It might make more sense to have a map of plugin identifiers → plugin API objects, and make 'Core' just one of them. Plugin API stubs could then just be exported like so:

### AuriservePluginCore.ts
```javascript
import type CoreType from 'auriserve-plugin-core-typedefs';
export default Core = _AURISERVE.getCoreApi() as any as CoreType;
```

~~### PluginStub.ts~~
```javascript
import AuriServe from 'auriserve-plugin-core'
import type PluginNameTypes from 'plugin-name-typedefs';

export default AuriServe.require('plugin-name') as API;
```

~~And requireApi could throw an error if the API can't be found.
I'd like a way to do this with TypeScript without unnecessary stubs. I suppose the stubs are only for TypeScript, and in JavaScript you could just use the `AuriServe.require` function raw.~~

Never mind, scratch all of that. Typescript lets you merge declarations [as seen here](https://www.typescriptlang.org/docs/handbook/declaration-merging.html#:~:text=be%20the%20following%3A-,interface%20Document%20%7B,%7D,-Merging%20Namespaces) so I can just use `AuriServe.require` for everything~ perfect. You'll still need to get the type definitions, but luckily, that doesn't require any runtime code or imports :3

## New name for AuriServe

The name AuriServe is dumb. Maybe Servo, Tinker, 