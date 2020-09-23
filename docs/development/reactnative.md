# React Native

## Add SVG support

1. Install the `react-native-svg-transformer` package

```bash
expo install react-native-svg
yarn add --dev react-native-svg-transformer
```

2. Create a `metro.config.js` file with the follwing content

```js
const { getDefaultConfig } = require("metro-config")

module.exports = (async () => {
  const {
    resolver: { sourceExts, assetExts },
  } = await getDefaultConfig()
  return {
    transformer: {
      babelTransformerPath: require.resolve("react-native-svg-transformer"),
    },
    resolver: {
      assetExts: assetExts.filter((ext) => ext !== "svg"),
      sourceExts: [...sourceExts, "svg"],
    },
  }
})()
```

3. Add the following to your `app.json` file

```json
{
  "expo": {
    "packagerOpts": {
      "config": "metro.config.js",
      "sourceExts": [
        "expo.ts",
        "expo.tsx",
        "expo.js",
        "expo.jsx",
        "ts",
        "tsx",
        "js",
        "jsx",
        "json",
        "wasm",
        "svg"
      ]
    }
  }
}
```
