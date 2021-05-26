## Optional: configuration for large or high data applications

```
verbose: boolean
```

By default, CodeSee instruments your code in order to record the data value of every expression. This always results in the application running slower while recording, and in rare circumstances, it can cause a noticeable slow down even when not recording. If this slowdown is happening in your application, you can configure CodeSee to use `verbose: false` (or terse) mode. CodeSee will instrument your code less and capture less data (just the inputs and outputs of functions), but continue to provide the same tracing, side effects, and visualizations as always.

- Verbose mode (default): gets all of the runtime data but in some applications or recordings can cause a noticeable slowdown.
- Terse mode: captures less runtime data, but your recordings will be more performant. If you have a high data application, or are noticing slowdown, we recommend you try setting `verbose: false`.


```json
"plugins": [
   ["@codesee/instrument", { "hosted": true, "verbose": false }],
   /* ... other dev plugins ... */
]
```

!!! note
    This setting affects all developers working on the application. It requires a clean build.