# Vite

## Create a vite project

```bash
yarn create vite app --template vue
```

## Install usefull packages

```bash
yarn add lodash
yarn add moment
```

## Install Quasar

```bash
yarn add quasar @quasar/extras
yarn add -D @quasar/vite-plugin sass@1.32.0
```

## Install and configure axios

```bash
yarn add axios vue-axios
```

in `main.js`

```js
import axios from 'axios'
import VueAxios from 'vue-axios'

...

app.use(VueAxios, axios)
```




## VS code plugins

- Vue Volar Extension Pack