# ESLint

## Initialize `eslint`

```bash
eslint --init
✔ How would you like to use ESLint?                        style
✔ What type of modules does your project use?              esm
✔ Which framework does your project use?                   vue
✔ Does your project use TypeScript?                        No
✔ Where does your code run?                                browser
✔ How would you like to define a style for your project?   prompt
✔ What format do you want your config file to be in?       JavaScript
✔ What style of indentation do you use?                    tab
✔ What quotes do you use for strings?                      single
✔ What line endings do you use?                            unix
✔ Do you require semicolons?                               No
```

## Fix issues

```bash
eslint --fix some_file
```

## Example `.eslintrc.js`

```js
module.exports = {
    'env': {
        'node': true,
        'es2020': true
    },
    'extends': [
        'eslint:recommended',
        'plugin:vue/essential'
    ],
    'parserOptions': {
        'ecmaVersion': 11,
        'sourceType': 'module'
    },
    'plugins': [
        'vue'
    ],
    'rules': {
        'indent': [
            'error',
            'tab'
        ],
        'linebreak-style': [
            'error',
            'unix'
        ],
        'quotes': [
   'error',
            'single'
        ],
        'semi': [
            'error',
            'never'
        ]
    }
}
```
