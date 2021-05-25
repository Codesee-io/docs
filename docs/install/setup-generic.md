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

```
verbose: boolean
```

By default, CodeSee instruments your code in order to record the data value of every expression. This always results in the application running slower while recording, and in rare circumstances, it can cause a noticeable slow down even when not recording. If this slowdown is happening in your application, you can configure CodeSee in `verbose: false` (or terse) mode. CodeSee will instrument your code less and capture less data (just the inputs and outputs of functions), but continue to provide the same tracing, side effects, and visualizations as always.

- Verbose mode (default): Gets all of the runtime data but in some applications or recordings can cause a noticeable slowdown.
- Terse mode: Captures less runtime data, but your recordings will be more performant. If you have a high data application, or are noticing slowdown, we recommend you try setting `verbose: false`.

Note: this setting is for all developers of the application, and changing it will require a clean build.

```
"plugins": [
   ["@codesee/instrument", { "hosted": true, "verbose": false }],
   /* ... other dev plugins ... */
]
```


## Next step: 

[Rebuild and run your app](../installation/#step-3-rebuild-and-run-your-app-locally)

 
