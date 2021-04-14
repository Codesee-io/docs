# Configuring CodeSee with Create React App

We're going to add [React App Rewired](https://github.com/timarney/react-app-rewired) following the instructions below. Please note that these instructions are slightly different than the ones on the react-app-rewired site. But, if you already have react-app-rewired installed, nothing to worry about here, you can skip to "Step 2) Create a config-overrides.js file".

#### 1) Install react-app-rewired

##### For create-react-app 2.x with Webpack 4:

```bash
$ npm install react-app-rewired --save-dev
```

##### For create-react-app 1.x or react-scripts-ts with Webpack 3:

```bash
$ npm install react-app-rewired@1.6.2 --save-dev
```

#### 2) Create a `config-overrides.js` file in the root directory

The configuration differs slightly based on the version of Create React App you are running.

<details><summary>Version 4.x.x</summary>

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

</details>

<details><summary>Version 3.x.x and 2.x.x</summary>

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

</details>


```
+-- your-project
|   +-- config-overrides.js
|   +-- node_modules
|   +-- package.json
|   +-- public
|   +-- README.md
|   +-- src
```

#### 3) 'Flip' the existing calls to `react-scripts` in `npm` scripts for start and build
```diff
  /* package.json */

  "scripts": {
-   "start": "react-scripts start",
+   "start": "react-app-rewired start",
-   "build": "react-scripts build",
+   "build": "react-app-rewired build",
    "test": "react-scripts test",
    "eject": "react-scripts eject"
}
```

Note: Please avoid setting this call for the `eject` and `test` scripts.

#### [Next step: Rebuild and run your app](/installation/#step-3-rebuild-and-run-your-app-locally)