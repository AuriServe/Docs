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

### PluginStub.ts
```javascript
import Core from 'auriserve-plugin-core'
import type PluginNameTypes from 'plugin-name-typedefs';

export default Core.api.require('plugin-name') as API;
```

And requireApi could throw an error if the API can't be found.
