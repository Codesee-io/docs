We will be adding configuration options over time.

## **`includeLibs`**
By default, CodeSee avoids instrumenting library code imported into your app. However, if you would like to see CodeSee data flows that include your framework, we are beginning to support that. Add the `includeLibs` option to the @codesee/instrument plugin config like so:

```
    plugins: [
      ["@codesee/instrument", {"includeLibs": ["gatsby"]}],
      <other plugins>
    ]
```

Currently, this option allows the following libraries:
- "gatsby"

## **`hosted`**

By default, CodeSee will run locally on your Docker container. In order to run it with our hosted version, add the `hosted` option to the @codesee/instrument plugin config like so:

```
    plugins: [
      ["@codesee/instrument", {"hosted": true}],
      <other plugins>
    ]
```

