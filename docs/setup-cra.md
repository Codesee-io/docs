---
hide:
  - toc
---
# Configuring CodeSee with Create React App

We're going to add [React App Rewired](https://github.com/timarney/react-app-rewired) following the instructions below. Please note that these instructions are slightly different than the ones on the react-app-rewired site. But, if you already have react-app-rewired installed, nothing to worry about here, you can skip to "Step 2) Create a config-overrides.js file".

#### 1) Install react-app-rewired

CodeSee supports Create React App 2.x or newer. If you're not sure what version you are using, you can check your package.json for the react-scripts dependency: its version is the same as your Create React App version!

```bash
$ npm install react-app-rewired --save-dev
```

#### 2) Create a `config-overrides.js` file in the root directory

The configuration differs slightly based on the version of Create React App you are running.

=== "Version 4.x.x"

    ```
    const webpack = require("webpack");

    module.exports = function override(config, env) {
      // add CodeSee babel plugin
      if (env === 'development') {
        const babelLoaderConfig = config.module.rules[1].oneOf[2];
        babelLoaderConfig.options.plugins.push(["@codesee/instrument", { hosted: true }]);
      }

      return config;
    }
    ```

=== "Version 3.x.x and 2.x.x"

    ```
    const webpack = require("webpack");

    module.exports = function override(config, env) {
      // add CodeSee babel plugin
      if (env === 'development') {
        const babelLoaderConfig = config.module.rules[2].oneOf[1];
        babelLoaderConfig.options.plugins.push(["@codesee/instrument", { hosted: true }]);
      }

      return config;
    }
    ```



```
+-- your-project
|   +-- config-overrides.js
|   +-- node_modules
|   +-- package.json
|   +-- public
|   +-- README.md
|   +-- src
```

#### 3) 'Flip' the calls to `react-scripts` in the `scripts` field of your `package.json`

In your package.json, your current `scripts` field should *currently* look a lot like this:

```
  /* package.json */

  "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test",
    "eject": "react-scripts eject"
}
```

Please change the `start` and `build` field to use `react-app-rewired` like this:

```
  /* package.json */

  "scripts": {
    "start": "react-app-rewired start",
    "build": "react-app-rewired build",
    "test": "react-scripts test",
    "eject": "react-scripts eject"
}
```

Note: Please avoid setting this call for the `eject` and `test` scripts.

#### [Next step: Rebuild and run your app](../installation/#step-3-rebuild-and-run-your-app-locally)

&nbsp;  