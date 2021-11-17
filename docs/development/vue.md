# Vue

## Install vue

```bash
npm install -g @vue/cli
```

## Create a project

```bash
vue create proj-name|.
```

> Make sure you use `yarn` as the package manager.

## Install required dependencies

```bash
yarn add -D @fortawesome/fontawesome-free
yarn add -D @mdi/font
yarn add vuex-persist
yarn add sprintf-js
yarn add vue-moment
yarn add moment-timezone
yarn add vue-js-modal
yarn add vue-uuid
yarn add vue-moment moment-timezone
yarn add vue-multiselect
```

## Add required files

```bash
touch .env
touch .env.development
touch .env.production
```

### Configure environment

```bash
vi .env.development
VUE_APP_API_URL = http://localhost:5000
```

```bash
vi .env.production
VUE_APP_API_URL = https://production.server.com
```

## Install required plugins

```bash
vue add vuetify
vue add i18n
vue add axios
```

## Run the development server

```bash
yarn serve
```

## Use required modules

## Import required stuff

In `main.js`:

```js
// ES5 conversion
// get rid of this: import '@babel/polyfill'
import 'core-js/stable'
import 'regenerator-runtime/runtime'

// Basics
import Vue from 'vue'
import App from './App.vue'
import router from './router'
import store from './store'
import vuetify from './plugins/vuetify'
import UUID from 'vue-uuid'
import VueMoment from 'vue-moment'
import moment from 'moment-timezone'

// Fonts
import 'roboto-fontface/css/roboto/roboto-fontface.css'
import '@fortawesome/fontawesome-free/css/all.css'
import '@mdi/font/css/materialdesignicons.css'

// Multiliguality
import i18n from './i18n'

// Additions
import VModal from 'vue-js-modal'
```

## Use required stuff

In `main.js`:

```js
Vue.use(UUID)
Vue.use(VModal)
Vue.use(VueMoment, { moment })
```

## Configure eslint

In `.exlintrc`:

```json
{
  "parser": "babel-eslint",
  "extends": ["plugin:vue/base"],
  "rules": {}
}
```

## Disable `eslint` while building

```bash
yarn remove @vue/cli-plugin-eslint
```

## Configure eslint and prettier for `vue`

1. Create a `.eslintrc.json` in your projects directory with the following content:

```json
{
  "parser": "vue-eslint-parser",
  "parserOptions": {
    "parser": "babel-eslint"
  },
  "plugins": ["vue", "prettier"],
  "extends": ["eslint:recommended", "plugin:vue/recommended"],
  "rules": {
    "indent": ["error", 2],
    "linebreak-style": ["error", "unix"],
    "quotes": ["error", "single"],
    "semi": ["error", "never"],
    "max-len": [
      "error",
      180,
      2,
      {
        "ignoreComments": false,
        "ignoreRegExpLiterals": true,
        "ignoreStrings": false,
        "ignoreTemplateLiterals": false
      }
    ],
    "vue/max-attributes-per-line": "off",
    "vue/html-closing-bracket-newline": [
      "error",
      {
        "singleline": "never",
        "multiline": "never"
      }
    ]
  }
}
```

2. Create a `.prettierrc` in your project directory with the following content:

```json
{
  "singleQuote": true,
  "printWidth": 150,
  "trailingComma": "none",
  "arrowParents": "always",
  "semi": false,
  "jsxBracketSameLine": true
}
```

3. Configure the project `settings.json` to use `.eslintrc.json`

```json
{
  "eslint.options": {
    "configFile": ".eslintrc.json"
  }
}
```

## Use git version and revision inside the app

1. Add and configure the `git-revision-webpack-plugin` in your `vue.config.js`.

```js
const pkg_json = require('./package.json')
// incuding the following line will use the version from package.json
// process.env.VUE_APP_VERSION = pkg_json.version;
process.env.VUE_APP_RELEASE_NAME = pkg_json.releaseName

const GitRevisionPlugin = require('git-revision-webpack-plugin')

module.exports = {
  chainWebpack: config => {
    config.plugin('define').tap(args => {
      const gitRevisionPlugin = new GitRevisionPlugin()
      args[0]['process.env']['VUE_APP_VERSION'] = JSON.stringify(gitRevisionPlugin.version())
      // If you also want to use the latest commit hash
      // args[0]['process.env']['VUE_APP_COMMITHASH'] = JSON.stringify(gitRevisionPlugin.commithash())
      // If you also want to use the branch name!
      // args[0]['process.env']['VUE_APP_BRANCH'] = JSON.stringify(gitRevisionPlugin.branch())
      // The following line is supported if you are using webpack v5 or later
      // args[0]['process.env']['VUE_APP_LASTCOMMITDATETIME'] = JSON.stringify(gitRevisionPlugin.lastcommitdatetime())
      return args
    })
  }
}
```

2. In the `package.json` file add or set the following values:

```json
{
  "version": "0.2.0",
  "releaseName": "beta 2",
}
```

3. In your `app_config.js` export the values as global variables:

```js
export const appVersion = process.env.VUE_APP_VERSION
export const releaseName = process.env.VUE_APP_RELEASE_NAME
```

4. Use the values inside a component:

```html
<template>
  <div>
    {{ appVersion }} ({{ releaseName }})
  </div>
</template>
```

```js
import { appVersion, releaseName } from '@/app_config'

export default {
  data() {
    return {
      appVersion,
      releaseName
    }
  }
}
```