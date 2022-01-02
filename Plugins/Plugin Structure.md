# Plugin Structure

A Plugin, in its barest form, is simply a folder containing a JavaScript source file for AuriServe to `require` and a [[Plugin Manifest]] identifying it.



Many developers take an isomorphic approach to Plugin development, in which they have one code base with several different entry points, and use a bundler such as Webpack to build 