# Plugin Manifest

A plugin's `manifest.yaml` is a YAML file containing information relating to a Plugin. Every plugin requires a `manifest.yaml` following the specification outlined below, and, unless specified otherwise, all keys are required.

YAML is parsed according to [[YAML|AuriServe's YAML parsing rules]].

## Specification & Example

```yaml
# The main identifier for your plugin. Must only contain 
# lowercase letters and hyphens. Should be the same as the 
# exported API identifier, if there is one.

identifier: my-auriserve-plugin

# Optional: The friendly name for your plugin, shown to users.
# May contain any characters, but it is recommended to keep it below
# 20 characters long, as any more than that may cause truncation.

name: My AuriServe Plugin

# Optional: A short description for your plugin. 
# May contain any characters, and span multiple lines.

description:|
	This is my awesome plugin for awesome things.
	Can you believe it?

# The author of the plugin. Must only contain letters and spaces,
# however, if an @ sign is the first character, the author is assumed
# to be an AuriServe Plugin Database Developer username, and it must
# conform to the format required there.

author: @Auri

# The SemVer version number of the plugin.

version: 0.5.2

# The list of entrypoints for the plugin.
# 'server' specifies code to run on the server, and 
# 'client' specifies code to run in the backend interface.
# The value can either be a string to the JavaScript file, or
# an object with the following keys:
# - script - The JavaScript file to execute.
# - style - A CSS Stylesheet to include (only valid on 'client')

entry:
- server: dist/server.js
- client:
	script: dist/editor.js
	style: dist/editor.css
```