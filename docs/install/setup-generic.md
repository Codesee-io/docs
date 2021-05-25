# Generic setup instructions

Follow these instructions if your project doesn't use one of the other specific environments listed.

--8<-- "snippets/install-first-step.md"

## Configure your project

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
If your project doesn’t include a babel config file (e.g. `.babelrc` or `babel.config.js`), you may have a babel configuration in your `webpack.config.js` file that you can add the `["@codesee/instrument", { "hosted": true }]` to. Look for an options block where your babel settings, presets, and plugins are being declared. Please add `["@codesee/instrument", { "hosted": true }]` to the list of your project's plugins as in the example below.

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


## Optional Config for Large or High Data Applications:

If you have a large, enterprise or high data application, we recommend to set the data verbosity to `false`. By default data verbosity is set to true. 


```
"plugins": [
   ["@codesee/instrument", { "hosted": true, "verbose": false }],
   /* ... other dev plugins ... */
]
```


--8<-- "snippets/install-last-step-rebuild.md"




 
