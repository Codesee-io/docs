---
hide:
  - toc
---
# Upgrading hosted to the latest version

1. From the root of your app, install the latest CodeSee packages:

    === "npm"

        ```
        npm install --save-dev @codesee/tracker@latest @codesee/babel-plugin-instrument@latest
        ```

    === "yarn"

        ```
        yarn add --dev @codesee/tracker@latest @codesee/babel-plugin-instrument@latest
        ```


2. Rebuild your app, and start your app development mode


## Troubleshooting
With some codebases, you'll need to clear your babel cache in order to see the latest changes immediately. Most babel caches are stored in:
- `node_modules/.cache/babel-loader`
- `.next/cache/next-babel-loader`

You can `rm -rf` this directory and rebuild or restart your app.
