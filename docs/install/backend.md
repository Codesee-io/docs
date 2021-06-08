If you want to run CodeSee in a backend application (such as a Node.js app), you need to configure it to start recording automatically.

There are two options. Either:

- Set the environment variable `CODESEE_RECORD_ON_START` to `true`
- Use webpack's DefinePlugin (or similar) to set up a find-replace for `"CODESEE_RECORD_ON_START": "true"` or `"process.env.CODESEE_RECORD_ON_START": "true"`.

For example, on the command line:

```shell
CODESEE_RECORD_ON_START=true node codesee/index.js
```

For example, in webpack:

```js
const webpack = require('webpack');

module.exports = {
  ...
  plugins: [
    new webpack.DefinePlugin({
      CODESEE_RECORD_ON_START: "true"
    })
  ]
};
```
