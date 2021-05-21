# Changing from local to hosted CodeSee

If you're running CodeSee locally but want to use the hosted option instead, you'll need to upgrade your version of CodeSee in slightly different ways, depending on what file your Babel intergration is in.

While this process will not delete any previous CodeSee recordings, you'll need to switch back to the local hosted option to access recordings previously recorded with CodeSee Local.

## Update the CodeSee dependencies

Update the devDependencies in your `packages.json` file to reflect the current CodeSee version. You can run either of these commands to update:

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
If you're using CodeSee with a Create React App application, you'll make these changes in the `config-overrides.js` file. Before updating, your `config-overrides.js` file should look something like this:

```
module.exports = function override(config, env) {
  // add CodeSee babel plugin
  if (env === 'development') {
    const babelLoaderConfig = config.module.rules[1].oneOf[2];
    babelLoaderConfig.options.plugins.push("@codesee/instrument");
  }
  return config;
}
```

Alter this text to add `{hosted: true}` to your CodeSee plugin. If `"@codesee/instrument"` is not currently wrapped in its own array in your file, you will need to do so, as shown below. If it is already wrapped in its own array as shown here `["@codesee/instrument"]`, please add `{hosted: true}` to the array as shown below.

```
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

Navigate to the file that you've added your CodeSee plugin to. You can search for `"@codesee/instrument"` to quickly find the correct file. For example, if you've added CodeSee to your `.babelrc` file, open your `.babelrc` file. It should contain text that looks similar to this.


```
  "env": {
    "development": {
      "plugins": [
        /* other plugins may be listed here */
        "@codesee/instrument"
      ],
    }
  }
```

Alter this text to add `{hosted: true}` to your CodeSee plugin. If `"@codesee/instrument"` is not currently wrapped in its own array in your file, you will need to do so, as shown below. If it is already wrapped in its own array as shown here `["@codesee/instrument"]`, please add `{hosted: true}` to the array as shown below.

```
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

You'll next need to clear `localStorage`. Open your application in your browser, making sure that the CodeSee floating action button is visible:

![CodeSee button running in web app](/img/codesee_button.png)

Right click on any point of your application in your browser and select inspect, to open Chrome developement tools.

Click on the Application option in your Chrome development tools. Then navigate to your local storage option in the left hand navigation menu.

Look for `http://localhost:5198`, right click on it and choose clear:

![Resetting local storage in Chrome DevTools](/img/remove_local_storage.png)
 
