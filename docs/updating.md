#Upgrading to CodeSee Hosted

You'll need to upgrade your version of CodeSee in slightly different ways, depending on what file your Babel intergration is in.

While this process will not delete any previous CodeSee recordings, you'll need to switch back to the local hosted option to access recordings previously recorded with CodeSee local.

## Updating with Create React App
If you're using CodeSee with a Create React App application, you'll make these changes in the config-overrides.js file. Before updating, your config-overrides.js file should look something like this:

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

Alter this text to add {hosted: true} to your CodeSee plugin as shown below.

```
module.exports = function override(config, env) {
  // add CodeSee babel plugin
  if (env === 'development') {
    const babelLoaderConfig = config.module.rules[1].oneOf[2];
    babelLoaderConfig.options.plugins.push(["@codesee/instrument", {hosted: true}]);
  }
  return config;
}
```


Next, update the devDependencies in your packages.json file to reflect the current CodeSee version. The most recent version of CodeSee is 0.17.0. Once updated, your code should look like this.


``` 
    "@codesee/babel-plugin-instrument": "0.17.0",
    "@codesee/tracker": "0.17.0"
``` 

If you're updating from a version of CodeSee with local storage to hosted, you'll next need to open your application in your browser, making sure that the CodeSee floating action button is visible.

Right click on any point of your application in your browser and select inspect, to open Chrome developement tools.

Click on the Application option in your Chrome development tools. Then navigate to your local storage option in the left hand navigation menu.

Look for http://localhost:5198, right click on it and choose clear.



## Updating other application types

First we'll need to set your version of CodeSee to hosted.

Navigate to the file that you've added your CodeSee plugin to. You can search for “@codesee/instrument” to quickly find the correct file. For example, if you've added CodeSee to your .babelrc file, open your .babelrc file. Your .babelrc file should contain text that looks similar to this.


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

Alter this text to add {hosted: true} to your CodeSee plugin as shown below.

If “@codesee/instrument” is not currently wrapped in its own array in your file, you will need to do so, as shown below. If it is already wrapped in its own array as shown here [“@codesee/instrument”], please add {hosted: true} to the array as shown below.

```  
  "env": {
    "development": {
      "plugins": [
        /* other plugins may be listed here */
        ["@codesee/instrument", {hosted: true}]
      ],
    }
  }
```




Next, let's update your version of CodeSee to the latest release. You can do this npm by typing [add from instructions]. Or via yarn using ['add from other instructions']

Next, open your application in your browser, making sure that the CodeSee floating action button is visible.
['show a screenshot of an application open with an arrow to the floating action button']

Right click on any point of your application in your browser and select inspect, to open Chrome developement tools.

Click on the Application option in your Chrome development tools. Then navigate to your local storage option in the left hand navigation menu.
['include screenshot with arrows']

Look for http://localhost:5198, right click on it and choose clear.




