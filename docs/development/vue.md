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
# yarn add -D eslint eslint-plugin-vue@next
yarn add vuex-persist
# yarn add axios vue-axios (not sure)
yarn add sprintf-js
yarn add vue-moment
yarn add moment-timezone
yarn add vue-js-modal
yarn add vue-uuid
yarn add vue-moment moment-timezone
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
# vue add moment (not sure)
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
