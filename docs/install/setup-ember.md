# Ember installation instructions (experimental!)

**WARNING:** Ember support is very early and experimental. At this point, we've only tested on a couple of relatively simple apps. If you are willing to give this a shot on your codebase, we would love to hear about your experience so we can continue to improve support.

--8<-- "snippets/install-first-step.md"

## Configure your project

We'll need to modify your babel config, and import `@codesee/tracker` both which we can do in the `ember-cli-build.js` file.  Here is an example structure that should work well for your app. Note that:
1. We detect development mode
2. We construct an object that is our babel options, and pass that into the EmberApp constructor. Then, only in development mode, we add `@codesee/instrument` to the list of babel plugins, along with the `frameworks: ["ember"]` option.
3. Only in development mode, we use `app.import` to load the `@codesee/tracker/build/codesee.web.hosted.js` npm package. (Note that for a local install, please import `@codesee/tracker/build/codesee.web.js` instead.)

```
module.exports = function (defaults) {
  const isDevelopment = process.env.EMBER_ENV === 'development';

  let babel = {
    /* If you have any existing babel configuration, move it here */
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

--8<-- "snippets/install-last-step-rebuild.md"


