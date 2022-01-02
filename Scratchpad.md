# Elements shouldn’t be built in to the system.
Preact shouldn’t be built into the system???

On the server-side, there could be a plugin that enables the [[Elements]] API, including the registry, and the parsing of them. On the client side, there’s no reason that Preact has to be sent by the server, it could (again) be injected by the client. An [[Injection]] API should exist for that, although I’m unsure if it should be in the core or if it should be a member of a Views add-on plugin. On the Admin side, it gets a little weirder, since I use contexts to pass down state that 