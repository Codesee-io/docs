---
hide:
  - toc
---
# Configuring CodeSee with Gatsby

**CodeSee is compatible with Gatsby 2.25.x+ or Gatsby 3.x.+**

1. You will need to follow [the instructions](https://www.gatsbyjs.com/docs/how-to/custom-configuration/babel/) for adding a `.babelrc` to your gatsby build if you have not already.
2. Once you've done that, add the "codesee" plugin for development. Add the following to the "env" -> "development" part of your config ("env" goes at the top level):
```
  "env": {
    "development": {
      "plugins": [
        ["@codesee/instrument", { "hosted": true }],
        /* ... other dev plugins ... */
      ]
    },
  }
```

#### [Next step: Rebuild and run your app](../installation/#step-3-rebuild-and-run-your-app-locally)

&nbsp;  
