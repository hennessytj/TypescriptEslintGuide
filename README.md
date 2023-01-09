# TypescriptEslintGuide

## Table of Contents

1. [Typescript npm project setup](https://khalilstemmler.com/blogs/typescript/node-starter-project/)

2. [Typescript eslint setup](https://khalilstemmler.com/blogs/typescript/eslint-for-typescript/)

3. [Typescript code formatting using prettier](https://khalilstemmler.com/blogs/tooling/prettier/)

4. Miscellaneous

## 1. Typescript npm project setup

### Setup package.json for project

```bash
$ npm init
```

#### Modify package.json scripts to include the following

```bash
"scripts": {
    "build": "tsc --build",
    "clean": "tsc --build --clean",
    "start": "npm run build && node build/index.js"
}
```

### Configure npm to work with Typescript

Note: @types/node configures ambient Typescript types which provide better autocompletion

```bash
$ npm install typescript @types/node --save-dev
```

### Configure tsconfig.json file

```bash
$ npx tsc --init --rootDir src --outDir build \
--esModuleInterop --resolveJsonModule --lib es6 \
--module commonjs --allowJs true --noImplicitAny true
```

## 2. Typescript eslint setup

### Install eslint, the typescript parser and typescript-eslint plugin

```bash
$ npm install --save-dev eslint @typescript-eslint/parser @typescript-eslint/eslint-plugin
```

### Create eslint config file

```bash
$ touch .eslintrc
```

### Add the following to .eslintrc

```bash
{
  "root": true,
  "parser": "@typescript-eslint/parser",
  "plugins": [
    "@typescript-eslint"
  ],
  "extends": [
    "eslint:recommended",
    "plugin:@typescript-eslint/eslint-recommended",
    "plugin:@typescript-eslint/recommended"
  ]
}
```

### Create eslint config file to ignore linting specified files

```bash
$ touch .eslintignore
$ echo build >> .eslintignore
$ echo node_modules >> .eslintignore
```

### Add linting to package.json scripts

```bash
"scripts": {
    ...
    "lint": "eslint . --ext .ts"
    ...
}
```

### Add rules to .eslintrc (0: off, 1: warning, 2: error)

- [Eslint Rules Specification](https://eslint.org/docs/latest/rules/)
- [Shopify rules config](https://www.npmjs.com/package/@shopify/eslint-plugin)
- [Facebook rules config](https://www.npmjs.com/package/eslint-config-fbjs)
- [Other configs and plugins](https://github.com/dustinspecker/awesome-eslint)

```bash
"rules": {
    "no-console": 2,           // compile error for console.log
    "semi": ["error", "never"] // disallow semicolons
}
```

### Use a plugin to extend your config (e.g., shopify)

#### Install the plugin

```bash
$ npm install @shopify/eslint-plugin --save-dev
```

#### Update .eslintrc to use Shopify plugin

NOTE: the shopify plugin requires "parserOptions" to be provided

```bash
{
    ...
    "extends": [
        "plugin:@shopify/typescript",
        "plugin:@shopify/typescript-type-checking"
    ],
    "parserOptions": {
        "project": "tsconfig.json"
    },
    ...
}
```

## 3. Typescript code formatting using prettier

### Install prettier

[Prettier Config Docs](https://prettier.io/docs/en/configuration.html)

```bash
$ npm install --save-dev prettier
```

### Configure prettier

#### Create config file

```bash
$ touch .prettierrc
```

#### Add configuration rules

[Rules](https://prettier.io/docs/en/options.html)

```bash
{
  "semi": false,
  "trailingComma": "none",
  "singleQuote": true,
  "printWidth": 80
}
```

#### Add prettier to package.json

```bash
{
  "scripts": {
    ...
    "prettier-format": "prettier --config .prettierrc 'src/**/*.ts' --write"
  }
}
```


## 4. Miscellaneous

Build project without configuring package.json scripts.

```bash
$ npx tsc --build --clean
OR
$ npx tsc
```

### Other useful links

- [Eslint w/ typescript](https://thesoreon.com/blog/how-to-set-up-eslint-with-typescript-in-vs-code)
- [Eslint getting started](https://eslint.org/docs/latest/user-guide/getting-started)
