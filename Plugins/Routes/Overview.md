# Overview
Exposes an API to register objects implementing the Route interface to certain paths, and manages calling those objects when a user navigates to a certain path.

<br>

## API
The following functions and properties are exported as `routes`:

### BaseRoute
The BaseRoute abstract class, which implements simple routing functionality. Should be extended with a `render` method that returns an HTML string.

### root
The currently bound root route. May be null.

### error
The currently bound error route. May be null.

### createReq(req: AuriServe.Request): Req
Creates a Routes Req object from a raw AuriServe request.

### get(path: String): Promise<Route | null>
Returns the route at the given path. May return null if no route at said path exists.

### getRoot(): Promise<Route | null>
Returns the root route.

### setRoot(root: Route | null)
Sets the root route.

### setErrorRoute(route: Route | null)
Sets the error route.