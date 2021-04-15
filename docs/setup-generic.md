# Generic setup instructions
Follow these instructions if your project doesn't use one of the other specific environments listed.

1. If you don't have [babel compilation](https://babeljs.io/) setup in your app, you will need to add it. Please use [Babel's excellent guide](https://babeljs.io/setup) for getting set-up in your specific environments.
1. Once you've added your babel setup, add the "codesee" plugin for development. For example, if you have a .babelrc file, add the following to the "env" -> "development" part of your config ("env" goes at the top level):
```
  "env": {
    "development": {
      "plugins": [
        ["@codesee/instrument", { "hosted": true }],
        /* ... other dev plugins ... */
      ]
    },
  }
```
If your project does not include a .babelrc file and you have a webpack.config.js file instead, you can add the `["@codesee/instrument", { "hosted": true }]`, to this file. Look for an options block where your babel settings, presets, and plugins are being declared. Please add `["@codesee/instrument", { "hosted": true }]` to the list of your project's plugins as in the example below.

```
   options: {
      presets: [
        //your project's babel presets go here
      ],
      plugins: [
        ["@codesee/instrument", { "hosted": true }],
        //other babel plugins go here
      ],
    },
```

#### [Next step: Rebuild and run your app](../installation/#step-3-rebuild-and-run-your-app-locally)
