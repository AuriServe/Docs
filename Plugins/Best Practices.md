# Best Practices

When writing a plugin, there are several best practices that you can conform to to help provide a positive developer experience to other users – and potential contributors – of your plugin.

## Provide Type Declarations

By far and away the most helpful thing you can do if your plugin exposes an API is to provide comprehensive TypeScript type declarations. The easiest way to do this is to use TypeScript to author your plugin and export typings separately, but you can also opt to use JavaScript and manually create your declaration files if that's what you are comfortable with. However, if you manually create declaration files you must take extreme care to keep them accurate and complete, as incorrect type declarations are worse than no type declarations at all.

## Export APIs under your Plugin's identifier

It is much clearer for everyone involved if plugins providing APIs [[Context#export identifier String api Object|export]] under their own identifier. This way, other developers can know at a glance what your API is identified as, and don't have to dig through your docs, or code, before they've even started.

## Clean up after yourself

Your plugin should only initialize itself on `on_enable`, and it should clean up and unregister everything that it did on `on_disable`. Failing to do this will lead to hard to track bugs and strange behavior, and will result in your plugin not being accepted into the AuriServe Plugin Database.