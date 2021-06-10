# Configuring CodeSee with Next.js

--8<-- "snippets/install-first-step.md"

## Configure your project

You need to add CodeSee to your `.babelrc` or `babel.config.js`.

You either need to follow option A or option B. Check the root of your Next.js app for a `.babelrc` or `babel.config.js`.

* If none exists, follow [Option A: If you don't have a Babel config](#option-a-if-you-dont-have-a-babel-config).
* If one already exists, follow [Option B: Add CodeSee to your Babel config](#option-b-add-codesee-to-your-existing-babel-config).


### Option A: If you don't have a Babel config

If you don't have one, create a new `babel.config.js` file in the root of your Next.js app.


```js
module.exports = {
  "presets": ["next/babel"],
  "plugins": [],
  "env": {
    "development": {
      "plugins": [["@codesee/instrument", {"hosted": true}]]
    }
  }
}
```



### Option B: Add CodeSee to your existing Babel config

Open your `.babelrc` or `babel.config.js` file, and add the codesee plugin under `env` -> `development`. For example, if you started with the default `.babelrc` for Next.js:

```json
{
  "presets": ["next/babel"],
  "plugins": [],
}
```

then you can add CodeSee with:

```json
{
  "presets": ["next/babel"],
  "plugins": [],
  "env": {
    "development": {
      "plugins": [["@codesee/instrument", {"hosted": true}]]
    }
  }
}
```



--8<-- "snippets/config-large-high-data.md"

--8<-- "snippets/install-last-step-rebuild.md"

