# Generic setup instructions

Follow these instructions if your project doesn't use one of the other specific frameworks listed.

--8<-- "snippets/install-first-step.md"

## Configure your project

1. If you don't have [Babel compilation](https://babeljs.io/) set up in your app, you need to add it. Use [Babel's excellent guide](https://babeljs.io/setup) for getting set up in your environment.
1. Once you've added your Babel setup, add the `codesee` plugin for development. For example, if you have a `.babelrc` file, add the following to the `env` -> `development` part of your config (`env` goes at the top level):

```json
  "env": {
    "development": {
      "plugins": [
        ["@codesee/instrument", { "hosted": true }],
        /* ... other dev plugins ... */
      ]
    },
  }
```

If your project doesn’t include a Babel config file (for example, `.babelrc` or `babel.config.js`), you may have a Babel configuration in your `webpack.config.js` file that you can add the `["@codesee/instrument", { "hosted": true }]` to. Look for an options block where your Babel settings, presets, and plugins are declared. Add `["@codesee/instrument", { "hosted": true }]` to the list of your project's plugins as in the example below:

```json
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


--8<-- "snippets/install-last-step-rebuild.md"




 
