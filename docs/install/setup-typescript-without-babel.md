# Configuring CodeSee with a TypeScript project that doesn't currently use Babel

In these instructions, we describe how to set up a parallel build system using Babel so that your existing flow is unchanged. You can continue to use `tsc` to compile and run your TypeScript files the same as you've always done. You will add new `build:codesee` and `run:codesee` commands to your `package.json` specifically for CodeSee. They build your project and put the resulting artifacts into the `/codesee` directory.

--8<-- "snippets/install-first-step.md"

## Install packages

Install the packages needed for Babel. This allows you to convert your TypeScript code into JavaScript using Babel.

=== "npm"

    ```shell
    npm install --save-dev @babel/cli @babel/core @babel/plugin-proposal-class-properties @babel/plugin-proposal-object-rest-spread @babel/preset-env @babel/preset-typescript
    ```

=== "yarn"

    ```shell
    yarn add --dev @babel/cli @babel/core @babel/plugin-proposal-class-properties @babel/plugin-proposal-object-rest-spread @babel/preset-env @babel/preset-typescript
    ```

## Configure Babel

In the root of your project, create a `.babelrc` file with the following:

```json
{
  "presets": [
    "@babel/preset-env",
    "@babel/typescript"
  ],
  "plugins": [
    "@babel/proposal-class-properties",
    "@babel/proposal-object-rest-spread",
    // Set hosted: true when using CodeSee Hosted. 
    // This parameter defaults to false, so you can leave it out if using CodeSee Local.
    ["@codesee/instrument", { "hosted": true }]
  ]
}
```

## Create the `build` and `start` script commands

1. Add the following line to the `scripts` section of your `package.json`.

  ``` json
  "build:codesee": "./node_modules/.bin/babel ./<your-top-level-dir> --out-dir ./codesee --extensions '.ts' --source-maps inline",
  ```

  Replace `<your-top-level-dir>` with the top-level directory where your source code is stored.

2. Make a copy of the script command you normally use to run your project (often called `start`).
3. Name the copy `start:codesee`.
4. Modify `start:codesee` to look in the `/codesee` directory for your source code. 
  For example if you normally have:

  ```json
  "scripts": {
    ...
    "start": "node ./dist"
    ...
  }
  ```

  Change it to:

  ```json
  "scripts": {
    ...
    "start": "node ./dist"
    "start:codesee": "node ./codesee"

    ...
  }
  ```

## Test it out

Try out your new Babel-based build system for CodeSee:

=== "npm"

    ```shell
    npm run build:codesee
    ```
    ```shell
    npm run start:codesee
    ```

=== "yarn"

    ```shell
    yarn build:codesee
    ```
    ```shell
    yarn start:codesee
    ```


And your program should be running the same as always, but with a purple CodeSee eye on the page as well.

## Tidying up

You'll probably want to add `codesee/` to your `.gitignore` file, so you don't accidentally commit any of the Babel build products from the `/codesee` directory.

--8<-- "snippets/config-large-high-data.md"

--8<-- "snippets/install-last-step-rebuild.md"

