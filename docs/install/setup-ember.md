# Ember installation instructions (experimental!)

!!! warning
    Ember support is very early and experimental. At this point, we've only tested on a couple of relatively simple apps. If you are willing to give this a shot on your codebase, we would love to hear about your experience so we can continue to improve support.

--8<-- "snippets/install-first-step.md"

## Configure your project

You need to modify your Babel config, and import `@codesee/tracker`, both of which you can do in the `ember-cli-build.js` file.  Here is an example structure that should work well for your app. 

Note that:

* CodeSee detects development mode.
* CodeSee constructs an object that is your Babel options, and passes that into the EmberApp constructor. Then, only in development mode, we add `@codesee/instrument` to the list of Babel plugins, along with the `frameworks: ["ember"]` option.
* Only in development mode, we use `app.import` to load the `@codesee/tracker/build/codesee.web.hosted.js` npm package. For a local install, import `@codesee/tracker/build/codesee.web.js` instead.

```js
module.exports = function (defaults) {
  const isDevelopment = process.env.EMBER_ENV === 'development';

  let babel = {
    /* If you have any existing Babel configuration, move it here */
  };

  // Adds CodeSee instrumentation, but only in development mode
  if (isDevelopment) {
    babel.plugins = babel.plugins || [];
    babel.plugins.push( ["@codesee/instrument", {frameworks: ["ember"]}] );
  }

  let app = new EmberApp(defaults, {
    babel,
    /* Any additional EmberApp configuration for your app goes here */
  });

  // Loads CodeSee, but only when in development mode
  if (isDevelopment) {
    app.import('node_modules/@codesee/tracker/build/codesee.web.hosted.js');
  }


  /* ... */


  return app.toTree();
};
```

--8<-- "snippets/config-large-high-data.md"

--8<-- "snippets/install-last-step-rebuild.md"


