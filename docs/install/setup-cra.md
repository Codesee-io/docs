# Configuring CodeSee with Create React App

CodeSee supports Create React App 2.x or newer. If you're not sure what version you are using, you can check your `package.json` for the `react-scripts` dependency: its version is the same as your Create React App version.

You need to add [React App Rewired](https://github.com/timarney/react-app-rewired) to your project. Note that these instructions are slightly different to the ones on the react-app-rewired site. If you already have react-app-rewired installed, you can skip to [Step 2: Create a `config-overrides.js` file in the root directory](#step-2-create-a-config-overrides-js-file-in-the-root-directory).

--8<-- "snippets/install-first-step.md"

## Install react-app-rewired

```shell
$ npm install react-app-rewired --save-dev
```

## Create a `config-overrides-js` file in the root directory

The configuration differs slightly based on the version of Create React App you are running.

=== "Version 4.x"

    ```js
    module.exports = function override(config, env) {
      // add CodeSee babel plugin
      if (env === 'development') {
        const babelLoaderConfig = config.module.rules[1].oneOf[2];
        // Set hosted: true when using CodeSee Hosted. 
        // This parameter defaults to false, so you can leave it out if using CodeSee Local.
        babelLoaderConfig.options.plugins.push(["@codesee/instrument", { hosted: true }]);
      }

      return config;
    }
    ```

=== "Version 3.x and 2.x"

    ```js
    module.exports = function override(config, env) {
      // add CodeSee babel plugin
      if (env === 'development') {
        const babelLoaderConfig = config.module.rules[2].oneOf[1];
        babelLoaderConfig.options.plugins.push(["@codesee/instrument", { hosted: true }]);
      }

      return config;
    }
    ```

Your project root should now look like this:

```yaml
+-- your-project
|   +-- config-overrides.js
|   +-- node_modules
|   +-- package.json
|   +-- public
|   +-- README.md
|   +-- src
```

## Edit the calls to `react-scripts` in the `scripts` field of your `package.json`

In your `package.json`, your `scripts` field should currently look similar to this:

```json
  "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test",
    "eject": "react-scripts eject"
}
```

Change the `start` and `build` fields to use `react-app-rewired` like this:

```json
  "scripts": {
    "start": "react-app-rewired start",
    "build": "react-app-rewired build",
    "test": "react-scripts test",
    "eject": "react-scripts eject"
}
```

!!! Note
    Do not use react-app-rewired for the `eject` and `test` scripts.

--8<-- "snippets/config-large-high-data.md"

--8<-- "snippets/install-last-step-rebuild.md"


