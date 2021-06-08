We will add more configuration options over time.



## **`hosted`**

By default, CodeSee runs locally in a Docker container. In order to run it with our hosted version, add the `hosted` option to the @codesee/instrument plugin config like so:

```js
plugins: [
  ["@codesee/instrument", {"hosted": true}],
  // other plugins
]
```

## **`includeLibs`**

By default, CodeSee avoids instrumenting library code imported into your app. However, if you want to see CodeSee data flows that include your framework, we are beginning to support that. Add the `includeLibs` option to the `@codesee/instrument` plugin configuration:

```js
plugins: [
  ["@codesee/instrument", {"includeLibs": ["gatsby"]}],
  // other plugins
]
```

Currently, this option supports the following libraries:
- Gatsby
