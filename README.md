# How to create a react app
This is a summery of commands which you need to use to create a react app with
* TypeScript
* Prettier
* EsLint

You can find an example project in the `example-project` folder

## Create react app with TypeScript

```bash
npx create-react-app my-app --template typescript
```

## Adding EsLint
```bash
npm install eslint --save-dev
```

### Adding npm run commands
Open your `package.json` file and add
```bash
...
    "scripts": {
        ...
        "linter": "npx eslint . --ext .js,.jsx,.ts,.tsx"
        ...
    },
...
```

### Generate .eslintrc.json
```bash
npx eslint --init
```

Select:
* To check syntax, find problems, and enforce code style
* JavaScript modules (import/export)
* React 
* Does your project use TypeScript No/Yes -> Yes
* Browser
* Airbnb: https://github.com/airbnb/javascript
* JSON 
* install eslint-plugin-react -> Yes

### Adding npm run commands
Open your `package.json` file and add
```bash
...
    "scripts": {
        ...
        "code:check": "npx prettier --check .",
        "code:format": "npx prettier --write .",
        ...
    },
...
```

## Adding Prettier

### Install Prettier and plugins for eslint
```bash
npm install eslint-config-prettier eslint-plugin-prettier prettier --save-dev
```

### Add lines to `.eslintrc.json`
Open `.eslintrc.json` 

#### extends
Add the following line in `extends`:
```bash
"plugin:prettier/recommended"
```
`"extends"` should look now like this:
```bash
"extends": [
    "eslint:recommended",
    "airbnb",
    "plugin:react/recommended",
    "plugin:prettier/recommended"
],
```
#### rules
Add the following line in `rules`:
```bash
"react/react-in-jsx-scope": "off",
"no-use-before-define": "off",
"@typescript-eslint/no-use-before-define": ["error"],
"react/jsx-filename-extension": [1, { "extensions": [".tsx"] }]
```
`"rules"` should look now like this:
```bash
"rules": {
    "react/react-in-jsx-scope": "off",
    "no-use-before-define": "off",
    "@typescript-eslint/no-use-before-define": ["error"],
    "react/jsx-filename-extension": [1, { "extensions": [".tsx"] }]
}
```

#### env
Add the following line in `env`:
```bash
"jest": true
```
`"env"` should look now like this:
```bash
"env": {
    "browser": true,
    "es2021": true,
    "jest": true
},
```

## Resolve conflicts

### Missing file extension
To resolve an error like

```bash
ESLint: Missing file extension for "./App"(import/extensions)
```

install `eslint-import-resolver-typescript`

```bash
npm install eslint-import-resolver-typescript
```

and add this to settings 

```bash
"settings": {
    "import/resolver": {
        "typescript": {} // this loads <rootdir>/tsconfig.json to eslint
    },
}
```

and add this to `"parserOptions"`

```bash
    "project": "./tsconfig.json"
```

### Missing file extension "tsx"

To resolve an error like

```bash
ESLint: Missing file extension "tsx" for "./App"(import/extensions)
```

add this to your `rules` in `.eslintrc.json`

```bash 
"rules": {
   "import/extensions": [
      "error",
      "ignorePackages",
      {
        "js": "never",
        "jsx": "never",
        "ts": "never",
        "tsx": "never"
      }
   ]
}
```

## Resources
* https://create-react-app.dev/docs/adding-typescript/
* https://medium.com/how-to-react/config-eslint-and-prettier-in-visual-studio-code-for-react-js-development-97bb2236b31a
* https://prettier.io/docs/en/install.html
* https://github.com/typescript-eslint/typescript-eslint/blob/master/packages/parser/README.md

