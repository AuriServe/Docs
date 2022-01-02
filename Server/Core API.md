# Core API

## Accessing the Core API

AuriServe creates a global variable called `_AURISERVE`, which is an object containing the `getServerApi()` method. `getServerApi()` returns the Core API from the API registry, which, in a somewhat strange recursive fashion, allows access to the API registry itself. The methods listed below are all contained within the Core API.

## Methods

### require(identifier: String, version?: String)

Returns the API exported with the specified `identifier` from the API Registry, or throws an error if the API has not been registered. Plugins should always specify their dependencies in their `plugin.yaml` file, though, so these runtime errors should not happen in well-made plugins.

APIs are added using the [[#export identifier String api Object|export]] function, but the identifier 'core' has a special case where it returns the Core API itself. This is because the Core API is within the API registry. So technically, you can `require('core').require('core')...` as many times as you want, but please don't.

The `version` property is a semver version of the API to require. If it is not specified, a warning is printed to the terminal with the currently loaded version of that API. The only reason `version` is optional is to aid developers in getting the current version of an API. **Do not leave `version` blank in published Plugins.**

## export(identifier: String, api: Object)

Adds the specified `api` to the plugin registry, with the specified `identifier`. This can be used to give plugins access to functionality from another.

### on(event: [[#Lifecycle Event]], callback: Function)

Binds `callback` to the specified [[#Lifecycle Event]], `event`. Plugins should use this functionality to listen for certain changes in AuriServe. As a basic standard, plugins should bind a callback to `on_enable` to initialize the plugin, and another to `on_disable` to clean themselves up.

### once(event: [[#Lifecycle Event]], callback: Function)

Functions similarly to [[#on event Lifecycle Event callback Function|on]], except `callback` is only triggered once, and then it is unbound.

### off(event: [[#Lifecycle Event]], callback: Function)

Unbinds a `callback` that was bound using [[#on event Lifecycle Event callback Function|on]] or [[#once event Lifecycle Event callback Function|once]].

## Definitions

### Lifecycle Event

A string specifying a specific event in the server lifecycle to listen to, in functions like [[#on event Lifecycle Event callback Function|on]] and [[#once event Lifecycle Event callback Function|once]]. A list of lifecycle events are as follows:

- **on_enable** - Called when the current plugin is enabled.
- **on_disable** - Called when the current plugin is disabled.
- **on_plugin_enable** - Called when a plugin is enabled. Callback is passed the plugin identifier.
- **on_plugin_disable** - Called when a plugin is disabled. Callback is passed the plugin identifier.
- **before_plugin_disable** - Called right before a plugin is disabled. Callback is passed the plugin identifier.
- **before_server_stop** - When right before the server is stopped.