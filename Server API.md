# Server API

## Accessing the Server API

AuriServe creates a global variable called `_AURISERVE`, which is an object containing the `getServerApi()` method. `getServerApi()` returns the Server API from the API registry, which, in a somewhat strange recursive fashion, allows access to the API registry itself. The methods listed below are all contained within the Server API.

## Methods

### require(identifier: String, version?: String)

Retrieves 