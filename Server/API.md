# API

Provides methods to export, unexport, and require APIs registered by Plugins.

### require(identifier: String)

Returns an API exported with the specified `identifier` from the API registry, or throws an error if the API has not been registered. Plugins must specify all APIs they will `require` in the dependencies key of their `manifest.yaml` file. 

Instead of calling `require`, it is recommended to directly [[#Indexing the API Object|index the API object]] for the API desired, as this allows TypeScript to pick up on API type definitions.

As a speci


Returns the API exported with the specified `identifier` from the API Registry, or throws an error if the API has not been registered. Plugins should always specify their dependencies in their `manifest.yaml` file, though, so these runtime errors should not happen in well-made plugins.

APIs are added using the [[#export identifier String api Object|export]] function, but the identifier 'core' has a special case where it returns the Core API itself. This is because the Core API is within the API registry. So technically, you can `require('core').require('core')...` as many times as you want, but please don't.

The `version` property is a semver version of the API to require. If it is not specified, a warning is printed to the terminal with the currently loaded version of that API. The only reason `version` is optional is to aid developers in getting the current version of an API. **Do not leave `version` blank in published Plugins.**

## export(identifier: String, api: Object)

Adds the specified `api` to the plugin registry, with the specified `identifier`. This can be used to give plugins access to functionality from another.