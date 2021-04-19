# Configuring CodeSee with Next.js

We'll be adding CodeSee to your `.babelrc` or `babel.config.js`.

You either need to follow step A or step B. Check the root of your next.js app for a `.babelrc` or `babel.config.js`. 
 - If none exists, follow *Option A: If you don't have a babel config*
 - If one already exists, follow *Option B: Add CodeSee to your babel config*


## Option A. If you don't have a babel config

If you don't have one, let's create a new `babel.config.js` file in the root of your next.js app.

`babel.config.js`
```
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

And that's it! The next time you run your app in development mode, you should see a circle with the CodeSee eye in your webpage.

## Option B: Add CodeSee to your existing babel config
Open your `.babelrc` or `babel.config.js` file, and add the codesee plugin under `env`/`development`. For example, if you started with the default `.babelrc` for next.js:

```
{
  "presets": ["next/babel"],
  "plugins": [],
}
```

then you can add CodeSee with:

```
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

And that's it! The next time you run your app in development mode, you should see a circle with the CodeSee eye in your webpage.
