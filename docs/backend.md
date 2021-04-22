---
hide:
  - toc
---
If you'd like CodeSee to run on the backend, CodeSee needs to be configured to start recording immediately. This is how:

Two options, either:

- set the env variable `CODESEE_RECORD_ON_START` to `true`
- use webpack's DefinePlugin (or similar) to set up a find-replace for `"CODESEE_RECORD_ON_START": "true"` or `"process.env.CODESEE_RECORD_ON_START": "true"`

For example, on the command line:

`CODESEE_RECORD_ON_START=true node codesee/index.js`

For example, in webpack:

```
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

&nbsp;  