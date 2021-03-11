# Welcome to the CodeSee Alpha
Welcome!

## Overview
Today, CodeSee consists of a few pieces. As part of your install, you will:

* add two npm libraries to your javascript app:
    * a CodeSee babel plugin (@codesee/babel-plugin-instrument), which instruments your code to send data to the CodeSee server
    * the CodeSee Tracker library (@codesee/tracker), which actually sends the data to the CodeSee server

You will be able to create CodeSee recordings of your app as long as you have the CodeSee babel plugin as part of your babel setup.

## Preparing your javascript app for CodeSee
### General instructions for CodeSee setup
1. From the root of your app, install the two codesee npm packages:
   - If you are using npm, run: `npm install --save-dev @codesee/tracker@0.13.1 @codesee/babel-plugin-instrument@0.13.1`
   - If you are using yarn, run: `yarn add --dev @codesee/tracker@0.13.1 @codesee/babel-plugin-instrument@0.13.1`


## CodeSee configuration for specific projects/environments
1. If you are not using any of the listed projects/environments, skip to the generic set up instructions

### Configuring CodeSee with Create React App

**Add React App Rewired**

Add [React App Rewired](https://github.com/timarney/react-app-rewired#how-to-rewire-your-create-react-app-project) to your project as described.

**Add CodeSee to config-overrides.js**

You should have created a `config-overrides.js` file in your project's root
directory as part of the React App Rewired install. Add the following to it:

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

### Configuring CodeSee with Babel and Typescript
In these instructions, we will set up a parallel build system using babel so that your existing flow will be unchanged. You will be able to continue to use `tsc` to compile and run your typescript files the same as you've always done. We will add new "build:codesee" and "run:codesee" commands to your package.json specifically for CodeSee. They will build your project and put the resulting artifacts into the /codesee directory.

**Install Packages**
We need to install the packages needed for babel. This will allow us to convert your typescript code into javascript using babel.
   - for npm: `npm install --save-dev @babel/cli @babel/core @babel/plugin-proposal-class-properties @babel/plugin-proposal-object-rest-spread @babel/preset-env @babel/preset-typescript
   - for yarn: `yarn add --dev @babel/cli @babel/core @babel/plugin-proposal-class-properties @babel/plugin-proposal-object-rest-spread @babel/preset-env @babel/preset-typescript

**Configure Babel**
In the root of your project, create a `.babelrc` file with the following:
```
{
  "presets": [
    "@babel/preset-env",
    "@babel/typescript"
  ],
  "plugins": [
    "@babel/proposal-class-properties",
    "@babel/proposal-object-rest-spread",
    /* ["@codesee/instrument", { hosted: true }] */ /* later, we will uncomment "@codesee/instrument" to introduce CodeSee instrumentation */
  ]
}
```

**Create the `build` and `start` script commands**
Add the following line to the "scripts" section of your `package.json`.

`"build:codesee": "./node_modules/.bin/babel ./src --out-dir ./codesee --extensions '.ts' --source-maps inline",`
Note: replace `./src` with the top-level directory where your source code is stored.

Now, make a copy the script command you normally use to run your project (often called `start`), name the copy `start:codesee` and modify it to look in the `/codesee` directory for your source code. For example if you normally have:

```
"scripts": {
  ...
  "start": "node ./dist"
  ...
}
```

Change it to:

```
"scripts": {
  ...
  "start": "node ./dist"
  "start:codesee": "node ./codesee"

  ...
}
```

**Test it out**
Reminder, we have *not* installed CodeSee. Only Babel.

Let's try out our new babel-based build system. Try:

For npm:

* `npm run build:codesee`
* `npm run start:codesee`

For yarn:

* `yarn build:codesee`
* `yarn start:codesee`

And your program should be running the same as it always has.

**Tidying up**
You'll probably want to add `codesee/` to your `.gitignore` file, so you don't accidentally commit any of the babel build products from the /codesee directory.

### Configuring CodeSee with Nuxt.js

You'll need to edit your `nuxt.config.js` to make sure the "codesee" babel plugin is included when in development mode.

**1. If you haven't already, store your config in a variable named `config`.**
That is, change from:

Before (in your `nuxt.config.js`)
```
export default {
  // ... your config goes here
}
```

After (in your `nuxt.config.js`)
```
const config = {
  // ... your config goes here
}

export default config;
```

**2. Add the following, which will ensure CodeSee runs when your app is run in development mode
The new code goes just before the `export default config;` line.**

In your `nuxt.config.js`:
```
// Use CodeSee instrumentation in development mode
if (process.env.NODE_ENV !== 'production') {
  const babel = config.build.babel = config.build.babel || {};
  const plugins = babel.plugins = babel.plugins || [];
  plugins.push(['@codesee/instrument', { hosted: true }]);

  const render = config.render = config.render || {};
  const bundleRenderer = render.bundleRenderer = render.bundleRenderer || {};
  bundleRenderer.runInNewContext = false;
}

export default config;
```
### Configuring CodeSee with Storybook
This configuration uses a custom storybook preset, which should be compatible with Storybook version 4.0.0 or newer.

**Place codesee-storybook-preset.js in your .storybook directory**

Copy `storybook/codesee-storybook-preset.js` from the codesee-alpha repository
into your `.storybook` directory.

**Add the preset to addons in main.js**

You should have a `main.js` in your `.storybook` directory.

You will need to add the following to the `addons` section of `main.js`:

```
path.resolve("./.storybook/codesee-storybook-preset.js")
```

If you haven't already, you may need to require the `path` module:
```
const path = require('path');
```

An example of a final `main.js` would look something like the following:

```
const path = require('path');

module.exports = {
  "stories": [
    "../src/**/*.stories.mdx",
    "../src/**/*.stories.@(js|jsx|ts|tsx)"
  ],
  "addons": [
    path.resolve("./.storybook/codesee-storybook-preset.js"),
    "@storybook/addon-links",
    "@storybook/addon-essentials",
    "@storybook/preset-create-react-app"
  ],
}
```
### Ember installation instructions

**WARNING:** Ember support is very early and experimental. At this point, we've only tested on a couple of relatively simple apps. If you are willing to give this a shot on your codebase, we would love to hear about your experience so we can continue to improve support.

We'll need to modify your babel config, and import `@codesee/tracker` both which we can do in the `ember-cli-build.js` file.  Here is an example structure that should work well for your app. Note that:
1. We detect development mode
2. We construct an object that is our babel options, and pass that into the EmberApp constructor. We add the @codesee/instrument babel plugin to those options with the `frameworks: ["ember"]` option, but only in development mode.
3. We use `app.import` to load the `@codesee/tracker` npm package, but only in development mode

```
module.exports = function (defaults) {
  const isDevelopment = process.env.EMBER_ENV === 'development';

  let babel = {
    /* If you have any existing babel configuration, move it here */
  };

  // Adds CodeSee instrumentation, but only in development mode
  if (isDevelopment) {
    babel.plugins ||= [];
    babel.plugins.push( ["@codesee/instrument", { hosted: true, frameworks: ["ember"]}] );
  }

  let app = new EmberApp(defaults, {
    babel,
    /* Any additional EmberApp configuration for your app goes here */
  });

  // Loads CodeSee, but only when in development mode
  if (isDevelopment) {
    app.import('node_modules/@codesee/tracker/build/codesee.js');
  }


  /* ... */

  return app.toTree();
};
```

## Generic babel setup instructions if your environment is not listed above
1. If you don't have [babel compilation](https://babeljs.io/) setup in your app, you will need to add it. Please use [Babel's excellent guide](https://babeljs.io/setup) for getting set-up in your specific environments.
1. Once you've added your babel setup, add the "codesee" plugin for development. For example, if you have a .babelrc file, add the following to "env":
```
  "env": {
    "development": {
      "plugins": [
        ['@codesee/instrument', { hosted: true }],
        /* ... other dev plugins ... */
      ]
    },
  }
```
If your project does not include a .babelrc file and you have a webpack.config.js file instead, you can add the `['@codesee/instrument', { hosted: true }]`, to this file. Look for an options block where your babel settings, presets and plugins are being declared. Please add `['@codesee/instrument', { hosted: true }]` to the list of your project's plugins as in the example below.

```
   options: {
      presets: [
        //your project's babel presets go here
      ],
      plugins: [
        ['@codesee/instrument', { hosted: true }],
        //other babel plugins go here
      ],
    },
```


**Did it work?**
1. Re-build your app and you should see the CodeSee eye icon towards the top right of your screen. Then you can celebrate!

## Updating to the latest version
WARNING: If you are updating from pre-0.7.0, this update will erase all your existing recordings. We do apologize! We will do our best to avoid this in the future.

1. In your local codesee-alpha directory, `git pull` the latest changes from this repo
2. Restart your docker compose by shutting down the docker container (Ctrl-C), and then running `docker-compose up` again.
3. From the root of your app, install the latest codesee packages:
   - If you are using npm, run: `npm install --save-dev @codesee/tracker@0.10.1 @codesee/babel-plugin-instrument@0.10.1`
   - If you are using yarn, run: `yarn add --dev @codesee/tracker@0.10.1 @codesee/babel-plugin-instrument@0.10.1`
4. Rebuild and restart your application

TROUBLESHOOTING ADVICE: If it appears that nothing has changed, your application may be cacheing its babel artifacts. If you can do a clean build, try that. Or, if not, try removing your `node_modules/.cache` directory, or even remove your entire `node_modules` directory.


## CodeSee options
We will be adding configuration options over time. Today, there is only a single one: `includeLibs`.

**`includeLibs`**
By default, CodeSee avoids instrumenting library code imported into your app. However, if you would like to see CodeSee data flows that include your framework, we are beginning to support that. Add the `includeLibs` option to the @codesee/instrument plugin config like so:

```
    plugins: [
      ["@codesee/instrument", {"hosted": true, "includeLibs": ["gatsby"]}],
      <other plugins>
    ]
```

Currently, this option allows the following libraries:
- "gatsby"



## Running CodeSee on the Backend
If you'd like CodeSee to run on the backend, CodeSee needs to start recording immediately. This is how:

Two options, either:
 - set the env variable `CODESEE_RECORD_ON_START` to `true`
 - use webpack's DefinePlugin (or similar) to set up a find-replace for `"CODESEE_RECORD_ON_START": "true"` or `"process.env.CODESEE_RECORD_ON_START": "true"`

For example, on the command line:

`CODESEE_RECORD_ON_START=true node codesee/index.js`

For example, in webpack:

```
const webpack = require('webpack');

module.exports = {
  ...
  plugins: [
    new webpack.DefinePlugin({
      CODESEE_RECORD_ON_START: "true"
    })
  ]
};
```
