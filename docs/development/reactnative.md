# React Native

## Upgrade `expo SDK`

```bash
npm i expo-cli -g --force
expo upgrade
... install required dependencies based on the npm output messages ...
expo client:install:ios
```

### Fixing upgrade

```bash
yarn install --check-files
watchman watch-del-all
rm -rf node_modules
expo install
yarn start -c
rm -rf /tmp/metro-*
```

### Fixing multiple react versions

> If you have errors depending on invalid hook call warnings.

```bash
yarn list react
```

If multiple react versions are installed:

> Be carefull! Linking react in expo projects does not fix the issue.

```bash
cd lib/node_module/react
yarn link
cd ../../../app
yarn link react
```

> For expo npm packages that are included:

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

## Add `moment.js` support

### Install `react-moment`

```bash
yarn add moment
yarn add react-moment
```

### Use `react-moment`

```jsx
import Moment from "react-moment" import { Text } from "react-native"

<Moment parse="x" format="YYYY/MM/DD" element={Text}>
  1234567890
</Moment>
```

## Add `.env` support to babel

&rarr; [Installation instructions](https://github.com/zetachang/react-native-dotenv/tree/master/babel-plugin-dotenv)

### Install `babel-plugin-dotenv`

```bash
yarn add babel-plugin-dotenv
```

### Configure `babel-plugin-dotenv`

In your `babel.config.js` add the following:

```js
{
  plugins: [["babel-plugin-dotenv", {
    "replacedModuleName": "babel-dotenv"
  }]]
}
```

### Use `babel-plugin-dotenv`

```js
import {API_URL, API_TOKEN} from "babel-dotenv"
```

## Build and deploy with expo

1. Adjust `app.json`
   At least the following properties:

```json
{
  "expo": {
    "version": "1.2.0",
    "updates": {
      "fallbackToCacheTimeout": 30000
    },
    "ios": {
      "bundleIdentifier": "unique.bundle.identifier",
      "buildNumber": "1.2.0"
    }
  }
}
```

2. Publish the app to the expo servers

```bash
expo publish
```

3. Build the app on expo servers

```bash
expo build:ios
```

4. Upload the app to the app store

```bash
expo upload:ios
```

Or use the `Transporter` app available in the [App Store](https://apps.apple.com/ch/app/transporter/id1450874784).

## Run app without development support

```bash
expo start --no-dev --minify
```

## Show logs from iPhone

### Installation

```bash
brew install --HEAD libimobiledevice -g
```

### Usage

```bash
idevicepair pair
idevicesyslog -q -K -m identifier|error|warn
```

## Expo eject

```bash
expo eject
cd ios
pod install
```

### Make sure the assets are copied correctly

You should return the following transformer in your `metro.config.js` file. If the file already exists before ejecting the
eject process will not adjust it correctly:

```js
module.exports = {
    transformer: {
        assetPlugins: ['expo-asset/tools/hashAssetFiles']
    }
};
```

### Deploy an ejected app
&rarr; Please goto [How to deploy a react native ios app on the app store](https://readybytes.in/blog/how-to-deploy-a-react-native-ios-app-on-the-app-store) for further information.
