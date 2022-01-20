# Views

## Overview

A View represents a template for rendering a page, or set of pages. For example, a Static Page View is provided by the Default Plugin, which takes a layout file (in HTML), and a tree of [[Elements]], and renders a single static page. Views may be more complex as well, representing trees such as Blogs or even entire E-Commerce frontends. Views integrate closely with [[Routes]], as they are the endpoints that Routes represent. To users, Views are displayed as options when a new Route is to be added.

This document details the Views export of the AuriServe module, which handles registering, unregistering, and managing views. It may be imported using Curly Imports (`import { Views } from 'AuriServe'`) or sub-modules (`import Views from 'AuriServe/Views'`).

## Methods

- **registerView(view: [[#View]])**



## Definitions

### View

- **identifier**: string
	A unique identifier for the view, containing the plugin name and the view name, separated by a colon. Both names should be snake_cased. Example: `auri_views:static_page`. This identifier should not change, as it is used to represent the element in all renderers.
	
- **name**: string
	A user-friendly name for the view. May contain any characters, including spaces. It is recommended to use Title Case and keep names under 20 characters.