# React

## Create a new react app

```bash
npx create-react-app my-app
cd my-app
cd src
rm -f *
touch index.css
touch index.js
cat <<EOF >> index.js
import React from 'react'
import ReactDOM from 'react-dom'
import './index.css'
EOF
yarn start
```