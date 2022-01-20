# Overview
Exposes a Preact instance to plugins.

<br>

## API
The following functions and properties are exported as `preact`:

### preact
The Preact instance, includes `h`, `createContext`, etc.

### hooks
The Preact hooks library, contains `useState`, `useEffect`, etc.

### forwardRef
The `forwardRef` function from `preact/compat`.

### renderToString
SSR Rendering function from `preact-render-to-string`.

<br>

## Globals
Currently, these globals are declared as a hack to fix Typescript & Webpack integration, and they will probably be removed once the underlying issue is fixed.

### \_\_AS_PREACT
[[#preact|The Preact export]].

## \_\_AS_PREACT_HOOKS
[[#hooks|The Preact Hooks export]].

### \_\_PREACT_COMPAT
The Preact Compat library, currently only contains `forwardRef`.

<br>

## Dependencies
(none)