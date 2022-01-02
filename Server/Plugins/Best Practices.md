# Best Practices

When writing a plugin, there are several best practices that you can conform to to help provide a positive developer experience to other users – and potential contributors – of your plugin.

## Provide Type Declarations

By far and away the most helpful thing you can do if your plugin exposes an API is to provide comprehensive TypeScript type declarations. The easiest way to do this is to use TypeScript to author your plugin and export typings separately, but you can also opt to use JavaScript and manually create your declaration files if that's what you are comfortable with. However, if you manually create declaration files you must take extreme care to keep them accurate and complete, as incorrect type decla