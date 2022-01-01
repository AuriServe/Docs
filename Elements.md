## Overview

An Element is a isolated container containing content, which may be static or interactive. They are, in essence, the building blocks of AuriServe. [[Views]] may use Elements to allow user-end editing, and to enable them to integrate with other plugins, and Plugins may provide and/or consume Elements as they see fit. For example, the Static Pages plugin allows users to compose pages out of Components, and the Blog plugin allows Elements to be added to Blog Posts. The Default plugin registers many core Elements for use, including Text Views, Column Layouts, Images, and more. Elements are versatile, and may be rendered on the Server, Client, or in the Administration Panel, depending on other plugin functionality, so care should be taken to make them function as smoothly as possible.

This document details the Elements export of the AuriServe module, which handles registering, unregistering, and managing elements. It may be imported using Curly Imports (`import { Elements } from 'AuriServe'`) or sub-modules (`import Elements from 'AuriServe/Elements'`).

## Methods

### registerElement(definition: [[#Element]])

Registers an element with the supplied `definition`. This element is added to the element registry, and may be accessed by [[Views]] and other plugins.

### unregisterElement(identifier: String): Boolean

Unregisters the element for the given `identifier`. This element is removed from the element registry, and can no longer be referenced or used. Returns true if the element existed and has been removed, false otherwise.

### getElement(identifier: String): [[#Element]] | `null`

Returns the element identified by `identifier`. If no matching element has been registered, returns `null`.

### listElements(): Map<identifier: String, element: [[#Element]]>

Returns a Map of all registered elements, indexed by their identifiers. Treat this Map as [[Definitions#Immutable|Immutable]]. If you need to modify an element definition, copy its current definition, unregister it, make your changes, and re-register it. 

### registerAlias(alias: string, identifier: String, transformer?: [[#Transformer Function]])

Registers an alias from `alias` to `identifier`. This should only be used if a previously registered element’s identifier had to change, such as if a plugin changes its name. Any elements identified by `alias` will be updated to be identified by `identifier`. This process is automatic, and irreversible. If supplied, `transformer` will be called on the element’s [[#Props]] before updating the element’s identifier. ^78cf71
	
### registerTransformer(definition: [[#Transformer]])

Registers a transformer with the supplied `definition`. A transformer represents the ability to *transform* one element to another, such as an image gallery to a carousel, and vice versa. Transformers represent an optional transformation. If a transformation is required for functionality e.g. when deprecating an element in favor of another, see [[#^78cf71|registerAlias]].

## Definitions

### Element

- **identifier**:  String
	A unique identifier for the element, containing the plugin name and the element name, separated by a colon. Both names should be snake_cased. Example: `auri_elements:rich_text`. Identifiers should remain stable between plugin versions. If they *must* change, an alias should be registered using [[#^78cf71|registerAlias]].
	
- **name**:  String
	A user-friendly name for the element. May contain any characters, including spaces. It is recommended to use Title Case and keep names under 20 characters.

- **element**: Preact Component
	The actual Preact element to render. This should differ depending on where the element is being registered. On the server, it should be a component that renders a static / hydratable element, on the client, it should be a component that hydrates the existing statically rendered element, and on the editor, it should be a component that can render from just the serialized props and include any editing widgets necessary.

### Transformer

- **from**: String
	The element identifier that the transformer transforms from.

- **to**: String
	The element identifier that the transformer transforms to.

- **title**?: String
	A title to display in menus. Defaults to “Convert to \[To Element Name\]”.

- **description**?: String
	A one or two line description to display in menus. Defaults to nothing. Use to add additional information such as warnings about lossy transformations.

- **check**: function(props: Object): Boolean
	A [[Definitions#Pure Function|Pure Function]] that can be executed to check if this transformation is valid. If supplied, the transformer will only be available if the function, when called with the element’s props, returns true. This function happens synchronously whenever Transformers are displayed, so avoid any intensive checks here. If intensive checks are needed, check them in `transform` and return `false` if the transformation is invalid, as described in [[#Transformer]].
	
- **transform**: [[#Transformer]]
	The transformer function to call on the element’s props when a transformation is requested.

### Transformer Function

function(props: [[#Props]]): Props | false

A [[Definitions#Pure Function|Pure Function]] used to transform an element’s props from one format to another. Used by [[#Transformer]] and [[#^78cf71|registerAlias]]. Accepts the current [[#Props]] of an element and must return a transformed [[#Props]] or `false` to indicate a failed transformation. Behavior on a failed transformation depends on the process that is using it.

### Props

A JSON-serializable JavaScript object that represents the static state, or properties of an element. Such properties define how the element renders, and the exact format of a Props object depends on the Element that it is for.

Numbers, Strings, Booleans, `null`, and Objects and Arrays of the aforementioned types are valid, other types are not. Do not store references to anything that will be invalidated between [[Views|View]] renders within Props.