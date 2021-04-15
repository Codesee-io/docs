# Configuring CodeSee with Nuxt.js

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

#### [Next step: Rebuild and run your app](../installation/#step-3-rebuild-and-run-your-app-locally)

&nbsp;  