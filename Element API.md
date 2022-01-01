## Methods

- **registerElement(definition: [[#Element Definition]])**
	Registers an element with the supplied definition.

- **registerElementAlias(alias:)


## Element Definition

- **identifier**
	A unique identifier for the element, containing the plugin name and the element name, separated by a colon. Both names should be snake_cased. Example: `auri_elements:text_view`. This identifier should not change, as it is used to represent the element in all renderers.
	
- **name**
	A user-friendly name for the element. May contain any characters, including spaces. It is recommended to use Title Case and keep names under 20 characters.

- **element**
	The actual React element to render. This should differ depending on where the element is being registered. On the server, it should be a component that renders a static / hydratable element, on the client, it should be a component that hydrates the existing statically rendered element, and on the editor, it should be a component that can render from just the serialized props and include any editing widgets necessary.

- **editing**
	An object containing additional properties relating to how the element behaves in the editor.

	**TODO: These properties should be refactored.**
	
	- **focusRing**
		Whether or not to render a default Focus Ring around the element. Set to false if rendering a custom Focus Ring with widgets.
	
	- **propertyEditor**
	- **inlineEditor**
