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
yarn add -D eslint eslint-plugin-vue@next
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
import "core-js/stable";
import "regenerator-runtime/runtime";

// Basics
import Vue from 'vue'
import App from './App.vue'
import router from './router'
import store from './store'
import vuetify from './plugins/vuetify'
import UUID from 'vue-uuid';
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
