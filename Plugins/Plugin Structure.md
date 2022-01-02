A Server Plugin is simply a folder containing JavaScript sources and a manifest file, which is loaded by AuriServe when requested by the user to augment server functionality. Plugins have full access to the NodeJS environment and the AuriServe [[Core API]], and can enhance and modify many areas of the system.

Many developers take an isomorphic approach to Plugin development, in which they have one code base with several different entry points, and use a bundler such as Webpack to build 