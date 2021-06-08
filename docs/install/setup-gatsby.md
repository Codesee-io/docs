# Configuring CodeSee with Gatsby

!!! note
    CodeSee is compatible with Gatsby 2.25.x+ or Gatsby 3.x.+

--8<-- "snippets/install-first-step.md"

## Configure your project

1. Follow [the instructions](https://www.gatsbyjs.com/docs/how-to/custom-configuration/babel/) for adding a `.babelrc` to your Gatsby build, if you have not already done so.
2. Add the `codesee` plugin for development. Add the following to the `env` -> `development` part of your config (`env` goes at the top level):

```js
  "env": {
    "development": {
      "plugins": [
        // Set hosted: true when using CodeSee Hosted. 
        // This parameter defaults to false, so you can leave it out if using CodeSee Local.
        ["@codesee/instrument", { "hosted": true }],
        /* ... other dev plugins ... */
      ]
    },
  }
```

--8<-- "snippets/config-large-high-data.md"

--8<-- "snippets/install-last-step-rebuild.md"



