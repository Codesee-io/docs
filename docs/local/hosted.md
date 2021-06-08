# Changing from CodeSee Local to hosted CodeSee

If you're running CodeSee locally but want to use the hosted option instead, you need to upgrade your version of CodeSee in slightly different ways, depending on what file your Babel intergration is in.

While this process does not delete any previous CodeSee recordings, you'll need to switch back to the local hosted option to access recordings previously recorded with CodeSee Local.

## Update the CodeSee dependencies

Update the `devDependencies` in your `packages.json` file to reflect the current CodeSee version. You can run either of these commands to update:

=== "npm"

    ```
    npm install --save-dev @codesee/tracker@latest @codesee/babel-plugin-instrument@latest
    ```

=== "yarn"

    ```
    yarn add --dev @codesee/tracker@latest @codesee/babel-plugin-instrument@latest
    ```

## Update the CodeSee tooling declaration

### Updating with Create React App

If you're using CodeSee with a Create React App application, make these changes in the `config-overrides.js` file. 

Before updating, your `config-overrides.js` file should look something like this:

```js
module.exports = function override(config, env) {
  // add CodeSee babel plugin
  if (env === 'development') {
    const babelLoaderConfig = config.module.rules[1].oneOf[2];
    babelLoaderConfig.options.plugins.push("@codesee/instrument");
  }
  return config;
}
```

Alter this code to add `{hosted: true}` to your CodeSee plugin:

```js
module.exports = function override(config, env) {
  // add CodeSee babel plugin
  if (env === 'development') {
    const babelLoaderConfig = config.module.rules[1].oneOf[2];
    babelLoaderConfig.options.plugins.push(["@codesee/instrument", {"hosted": true}]);
  }
  return config;
}
```

### Updating other application types

Navigate to the file that you've added your CodeSee plugin to. You can search for `"@codesee/instrument"` to quickly find the correct file. For example, if you've added CodeSee to your `.babelrc` file, open your `.babelrc` file. It should contain text that looks similar to this:

```json
  "env": {
    "development": {
      "plugins": [
        /* other plugins may be listed here */
        "@codesee/instrument"
      ],
    }
  }
```

Alter this text to add `{hosted: true}` to your CodeSee plugin:

```json
  "env": {
    "development": {
      "plugins": [
        /* other plugins may be listed here */
        ["@codesee/instrument", {"hosted": true}]
      ],
    }
  }
```

## Reset localStorage

You need to clear `localStorage`. 

1. Open your application in your browser, making sure that the CodeSee floating action button is visible:
  ![CodeSee button running in web app](../../img/codesee_button.png)
2. Open Chrome developement tools. You can do this through the appropriate keyboard shortcut for your system, or by right-clicking on the page and selecting **Inspect Element**.
3. Select the **Application** tab in your Chrome development tools. 
4. Browse to **Local Storage** in the left hand navigation menu.
5. Find **http://localhost:5198**, right click on it, and choose **Clear**.

![Resetting local storage in Chrome DevTools](../../img/remove_local_storage.png)
 
