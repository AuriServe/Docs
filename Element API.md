## Methods

The following methods are exposed under the `Elements` export of the `AuriServe` module, which is also available at `AuriServe/Elements`.

- **registerElement(definition: [[#Element Definition]])**
	Registers an element with the supplied `definition`. Elements are rendered portions of a [[View]]. They may be static content or interactive experiences. Elements are written and rendered in Preact both on the server and, in some cases, the client.

- **registerAlias(alias: string, identifier: string, transformer?: [[#Transformer Function]])**
	Registers an alias from `alias` to `identifier`. This should only be used if a previously registered element’s identifier had to change, such as if a plugin changes its name. Any elements identified by `alias` will be updated to be identified by `identifier`. This process is automatic, and irreversible.
	If supplied, `transformer` will be called on the element’s [[#Props]] before updating the element’s identifier. ^78cf71
	
- **registerTransformer(definition: [[#Transformer Definition]])**
	Registers a transformer with the supplied `definition`. A transformer represents the ability to *transform* one element to another, such as an image gallery to a carousel, and vice versa. Transformers represent an optional transformation. If a transformation is required for functionality e.g. when deprecating an element in favor of another, see [[#^78cf71|registerAlias]].

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

- **to:** string
	The element identifier that the transformer transforms to.

- **check:** function(props: any): boolean
	A [[Definitions#Pure Function|Pure Function]] that can be executed to check if this transformation is valid. If supplied, the transformer will only be available if the function, when called with the element’s props, returns true. This function happens synchronously whenever Transformers are displayed, so avoid any intensive checks here. If intensive checks are needed, check them in `transform` and return `false` if the transformation is invalid, as described in [[#Transformer Function]].
	
- **transform**: [[#Transformer Function]]
	The transformer function to call on the element’s props when a transformation is requested.

## Transformer Function
function(props: [[#Props]]): Props | false

A [[Definitions#Pure Function|Pure Function]] used to transform an element’s props from one format to another. Used by [[#Transformer Definition]] and [[#^78cf71|registerAlias]]. Accepts the current [[#Props]] of an element and must return a transformed [[#Props]] or `false` to indicate a failed transformation. Behavior on a failed transformation depends on the process that is using it.

## Props

A JSON-serializable JavaScript object that represents the static state, or properties of an element. Such properties define how the element renders, and the exact format of a Props object depends on the Element that it is for.

Numbers, Strings, Booleans, `null`, and Objects and Arrays of the aforementioned types are valid, other types are not. Do not store references to anything that will be invalidated between [[View]] renders within Props.