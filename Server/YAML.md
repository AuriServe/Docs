# YAML Parsing

Most config files in the AuriServe core are expressed using YAML, and plugins are encouraged to follow this convention themselves. YAML is used because it has increased readability compared to JSON, and it offers more flexibility with data representation.

## How YAML is parsed by AuriServe

YAML is parsed using the [js-yaml](https://www.npmjs.com/package/js-yaml) module for NodeJS, using the Failsafe Schema. This means that explicit tagging will not work, and that everything is interpreted as a String, Array, or Object. AuriServe will accept the strings 'true', 'false', and 'null' where appropriate, and it is not necessary to quote these values when inputting them as strings.

The full YAML syntax is available, but for reasons outlined in [this document](https://hitchdev.com/strictyaml/features-removed/), it is recommended to refrain from using duplicate keys, node anchors, and flow style, as these features generally lead to less readable documents and strange errors.

## How YAML should be parsed by Plugins

Plugin developers may `require` the YAML API using the [[Context]], which will enforce identical behavior to that in the AuriServe Core. If Plugin developers instead choose to roll their own YAML parsing library, it is their obligation to ensure consistency themselves.

## Where YAML is used

- [[Plugin Manifest|Plugin Manifests]]