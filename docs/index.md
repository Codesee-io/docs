# Welcome to the CodeSee Alpha
Welcome!

## Overview
Today, CodeSee consists of a few pieces. As part of your install, you will:

* run a local CodeSee server (see docker-compose instructions below)
* add two npm libraries to your javascript app:
  * a CodeSee babel plugin (@codesee/babel-plugin-instrument), which instruments your code to send data to the CodeSee server
  * the CodeSee Tracker library (@codesee/tracker), which actually sends the data to the CodeSee server
  
You will be able to create CodeSee recordings of your app so long as you have the CodeSee server running, and have the CodeSee babel plugin as part of your babel setup.

# Installation
## Account Setup
1. Get access to docker codeseeio/app_node, make sure to have Docker installed, and that you are logged in.
1. Get access to github.com/codesee-io/codesee-alpha, and git clone it locally. We recommend putting this repo *outside* of your app directory. For example:

- src/
  - my-app/
  - codesee-alpha/

```
git clone git@github.com:Codesee-io/codesee-alpha.git --depth=1
```

## CodeSee Server Setup
1. From the local, cloned codesee-alpha directory, run docker compose:
   `docker-compose up`
1. Wait for postgres to report it's ready to receive requests, then hit Control C to stop the server
1. When you're ready, run `docker-compose up` and your CodeSee server should be good to go. You'll know everything is working when you see the message: `server started at http://localhost:5198`

From now on, you can run `docker-compose up` in the codesee-alpha directory anytime to start up the CodeSee server, and \<ctrl\>+c to bring the server back down.



## Preparing your javascript app for CodeSee
### General instructions for CodeSee setup
1. From the root of your app, install the two codesee npm packages:
   - If you are using npm, run: `npm install --save-dev @codesee/tracker@0.10.1 @codesee/babel-plugin-instrument@0.10.1`
   - If you are using yarn, run: `yarn add --dev @codesee/tracker@0.10.1 @codesee/babel-plugin-instrument@0.10.1`


### CodeSee configuration for specific projects/environments
1. If you are not using any of the following projects/environments, skip to the generic set up instructions
* [Create React App](create-react-app/README.md)
* [TypeScript (without Babel)](typescript/README.md)
* [NuxtJS](nuxt/README.md)
* [Storybook (versions 4+)](storybook/README.md)
* [Ember (experimental)](ember/README.md)

### Generic babel setup instructions if your environment is not listed above
1. If you don't have [babel compilation](https://babeljs.io/) setup in your app, you will need to add it. Please use [Babel's excellent guide](https://babeljs.io/setup) for getting set-up in your specific environments.
1. Once you've added your babel setup, add the "codesee" plugin for development. For example, if you have a .babelrc file, add the following to "env":
```
  "env": {
    "development": {
      "plugins": [
        "@codesee/instrument",
        /* ... other dev plugins ... */
      ]
    },
  }
```
If your project does not include a .babelrc file and you have a webpack.config.js file instead, you can add the `"@codesee/instrument"`, to this file. Look for an options block where your babel settings, presets and plugins are being declared. Please add `"@codesee/instrument"` to the list of your project's plugins as in the example below.

```
   options: {
      presets: [
        //your project's babel presets go here
      ],
      plugins: [
        "@codesee/instrument",
        //other babel plugins go here
      ],
    },
```


### Did it work?
1. Re-build your app and you should see the CodeSee eye icon towards the top right of your screen. Then you can celebrate!

# Updating to the latest version
WARNING: If you are updating from pre-0.7.0, this update will erase all your existing recordings. We do apologize! We will do our best to avoid this in the future.

1. In your local codesee-alpha directory, `git pull` the latest changes from this repo
1. Restart your docker compose by shutting down the docker container (Ctrl-C), and then running `docker-compose up` again.
1. From the root of your app, install the latest codesee packages:
   - If you are using npm, run: `npm install --save-dev @codesee/tracker@0.10.1 @codesee/babel-plugin-instrument@0.10.1`
   - If you are using yarn, run: `yarn add --dev @codesee/tracker@0.10.1 @codesee/babel-plugin-instrument@0.10.1`
1. Rebuild and restart your application

TROUBLESHOOTING ADVICE: If it appears that nothing has changed, your application may be cacheing its babel artifacts. If you can do a clean build, try that. Or, if not, try removing your `node_modules/.cache` directory, or even remove your entire `node_modules` directory.


# CodeSee options
We will be adding configuration options over time. Today, there is only a single one: `includeLibs`. 

## `includeLibs`
By default, CodeSee avoids instrumenting library code imported into your app. However, if you would like to see CodeSee data flows that include your framework, we are beginning to support that. Add the `includeLibs` option to the @codesee/instrument plugin config like so:

```
    plugins: [
      ["@codesee/instrument", {"includeLibs": ["gatsby"]}],
      <other plugins>
    ]
```

Currently, this option allows the following libraries:
- "gatsby"



# Running CodeSee on the Backend
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
