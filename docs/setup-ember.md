---
hide:
  - toc
---
# Ember installation instructions (experimental!)

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
    app.import('node_modules/@codesee/tracker/build/codesee.web.hosted.js');
  }


  /* ... */

  return app.toTree();
};
```

#### [Next step: Rebuild and run your app](../installation/#step-3-rebuild-and-run-your-app-locally)

&nbsp;  
