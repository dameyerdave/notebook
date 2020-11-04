# ESLint

## Initialize `eslint`

```bash
node_modules/.bin/eslint --init
✔ How would you like to use ESLint?                        style
✔ What type of modules does your project use?              esm
✔ Which framework does your project use?                   vue
✔ Does your project use TypeScript?                        No
✔ Where does your code run?                                browser
✔ How would you like to define a style for your project?   prompt
✔ What format do you want your config file to be in?       JSON
✔ What style of indentation do you use?                    tab
✔ What quotes do you use for strings?                      single
✔ What line endings do you use?                            unix
✔ Do you require semicolons?                               No
```

## Fix issues

```bash
eslint --fix some_file
```

## Example `.eslintrc.json` for vue

```json
{
  "env": {
   "browser": true,
   "node": true,
   "es6": true
 },
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

## Example `.prettierrc` for vue

```json
{
    "singleQuote": true,
    "printWidth": 150,
    "trailingComma": "none",
    "arrowParents": "always",
    "semi": false,
    "jsxBracketSameLine": true,
    "tabWidth": 2
}
```