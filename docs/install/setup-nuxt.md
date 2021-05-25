# Configuring CodeSee with Nuxt.js

--8<-- "snippets/install-first-step.md"

## Configure your project

You need to edit your `nuxt.config.js` to make sure the `codesee` Babel plugin is included when in development mode.

## Store your config in a variable named `config`

That is, change from:

Before (in your `nuxt.config.js`)
```js
export default {
  // ... your config goes here
}
```

After (in your `nuxt.config.js`)
```js
const config = {
  // ... your config goes here
}

export default config;
```

## Edit your config to ensure CodeSee runs when your app is run in development mode

The new code goes just before the `export default config;` line.

In your `nuxt.config.js`:
```js
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

--8<-- "snippets/install-last-step-rebuild.md"
