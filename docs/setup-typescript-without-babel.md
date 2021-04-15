# Configuring CodeSee with a Typescript project that doesn't use Babel
In these instructions, we will set up a parallel build system using babel so that your existing flow will be unchanged. You will be able to continue to use `tsc` to compile and run your typescript files the same as you've always done. We will add new "build:codesee" and "run:codesee" commands to your package.json specifically for CodeSee. They will build your project and put the resulting artifacts into the /codesee directory.

**Install Packages**
We need to install the packages needed for babel. This will allow us to convert your typescript code into javascript using babel.

<details><summary>npm</summary>
```
npm install --save-dev @babel/cli @babel/core @babel/plugin-proposal-class-properties @babel/plugin-proposal-object-rest-spread @babel/preset-env @babel/preset-typescript
```
</details>

<details><summary>yarn</summary>
```
yarn add --dev @babel/cli @babel/core @babel/plugin-proposal-class-properties @babel/plugin-proposal-object-rest-spread @babel/preset-env @babel/preset-typescript
```
</details>

**Configure Babel**
In the root of your project, create a `.babelrc` file with the following:
```
{
  "presets": [
    "@babel/preset-env",
    "@babel/typescript"
  ],
  "plugins": [
    "@babel/proposal-class-properties",
    "@babel/proposal-object-rest-spread",
    ["@codesee/instrument", { hosted: true }]
  ]
}
```

**Create the `build` and `start` script commands**
Add the following line to the "scripts" section of your `package.json`.

`"build:codesee": "./node_modules/.bin/babel ./src --out-dir ./codesee --extensions '.ts' --source-maps inline",`

> Note: replace `./src` with the top-level directory where your source code is stored.

Now, make a copy the script command you normally use to run your project (often called `start`), name the copy `start:codesee` and modify it to look in the `/codesee` directory for your source code. For example if you normally have:

```
"scripts": {
  ...
  "start": "node ./dist"
  ...
}
```

Change it to:

```
"scripts": {
  ...
  "start": "node ./dist"
  "start:codesee": "node ./codesee"

  ...
}
```

**Test it out**

Let's try out our new babel-based build system for codesee. Try:

<details><summary>npm</summary>

```
npm run build:codesee
```
```
npm run start:codesee
```

</details>

<details><summary>yarn</summary>

```
yarn build:codesee
```
```
yarn start:codesee
```

</details>

And your program should be running the same as always, but with a purple CodeSee eye on the page as well.

**Tidying up**

You'll probably want to add `codesee/` to your `.gitignore` file, so you don't accidentally commit any of the babel build products from the /codesee directory.

#### [Next step: Rebuild and run your app](../installation/#step-3-rebuild-and-run-your-app-locally)

&nbsp;  