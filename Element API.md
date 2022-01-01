## Methods

The following methods are exposed under the `Elements` export of the `AuriServe` module, which is also available at `AuriServe/Elements`.

- **registerElement(definition: [[#Element Definition]])**
	Registers an element with the supplied `definition`. Elements are rendered portions of a [[View]]. They may be static content or interactive experiences. Elements are written and rendered in Preact both on the server and, in some cases, the client.

- **registerAlias(alias: string, identifier: string, transformer?: [[#Transformer Function]])**
	Registers an alias from `alias` to `identifier`. This should only be used if a previously registered element’s identifier had to change, such as if a plugin changes its name. Any elements identified by `alias` will be updated to be identified by `identifier`. This process is automatic, and irreversible.

- **registerTransformer(definition: [[#Transformer Definition]])**
	Registers a transformer with the supplied `definition`. A transformer represents the ability to *transform* one element to another, such as an image gallery to a carousel, and vice versa.


## Element Definition

- **identifier**:  string
	A unique identifier for the element, containing the plugin name and the element name, separated by a colon. Both names should be snake_cased. Example: `auri_elements:text_view`. This identifier should not change, as it is used to represent the element in all renderers.
	
- **name**:  string
	A user-friendly name for the element. May contain any characters, including spaces. It is recommended to use Title Case and keep names under 20 characters.

- **element**: Preact Component
	The actual React element to render. This should differ depending on where the element is being registered. On the server, it should be a component that renders a static / hydratable element, on the client, it should be a component that hydrates the existing statically rendered element, and on the editor, it should be a component that can render from just the serialized props and include any editing widgets necessary.

## Transformer Definition

- **from**: string
	The element identifier that the transformer transforms from.

