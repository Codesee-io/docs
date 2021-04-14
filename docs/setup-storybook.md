# Configuring CodeSee with Storybook
This configuration uses a custom storybook preset, which should be compatible with Storybook version 4.0.0 or newer.

**Place codesee-storybook-preset.js in your .storybook directory**

Copy the following into a new file called `codesee-storybook-preset.js`
inside your `.storybook` directory:

```
module.exports = {
  babel: async (config, options) => {
    if (options.configType === "DEVELOPMENT") {
      const plugins = config.plugins = config.plugins || [];
      plugins.push(['@codesee/instrument', { hosted: true }]);
    }
    return config;
  }
};
```

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