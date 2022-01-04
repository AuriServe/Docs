# API

The API object is a property of the root [[Context|Plugin Context]] which provides methods to export, unexport, and require APIs registered by other Plugins.

## Methods

### require(identifier: String)

Returns an API [[#export identifier String api Object|exported]] with the specified `identifier` from the API registry, or throws an error if the API has not been registered. Plugins must specify all APIs they require in the dependencies key of their `manifest.yaml` file. 

As a special case, requiring `core` will always return the root [[Context|Plugin Context]].

Instead of calling `require`, it is recommended to directly [[#Indexing the API Object|index the API object]] for the API desired, as this allows TypeScript to pick up on API type definitions.

### export(identifier: String, api: Object)

**Adds the specified `api` to the API registry under the specified `identifier`. Other plugins can use [[#require identifier String|require]] to access APIs registered this way to depend on other plugins' functionality.

Plugins should always export APIs under their own `identifier`. If a plugin tries to export an API with a different identifier, an error will be thrown unless an exclamation mark is put before the identifier in the string. **This should not be done except in extremely rare circumstances.**

### unexport(identifier: String)

Removes the API identified by `identifier` from the API registry. Returns a boolean indicating if an API existed by that identifier before deletion.

Plugins should always unexport APIs they exported on the [[`on_unload` event]].

## Indexing the API Object

When accessing APIs, it is best to index the API object directly, as Plugins can provide type definitions for their APIs this way. For example, instead of writing `auriserve.api.require('otherApi')`, it would be better to write `auriserve.api.otherApi`. This interally calls [[#require identifier String|require]], so the behavior is identical.