# Server API

## Accessing the Server API

AuriServe creates a global variable called `_AURISERVE`, which is an object containing the `getServerApi()` method. `getServerApi()` returns the Server API from the API registry, which, in a somewhat strange recursive fashion, allows access to the API registry itself. The methods listed below are all contained within the Server API.

## Methods

### require(identifier: String, version?: String)

Returns the API exported with the specified `identifier` from the API Registry, or throws an error if the API has not been registered. Plugins should always specify their dependencies in their `plugin.yaml` file, though, so these runtime errors should not happen in well-structured codebases.

APIs are added using the [[#expose]] function, but the identifier 'core' has a special case where it returns the Server API itself. This is because the Server API is within the API registry. So technically, you can `require('core').require('core')...` as many times as you want, but please don't.

The `version` property is a semver version of the API to require. If it is not specified, a warning is printed to the terminal with the currently loaded version of that API. The only reason `version` is optional is to aid developers in getting the current version of an API. **Do not** leave `version` blank in published Plugins.