# Usage of Husky with Prettier and Eslint

This document describes how to use Husky with Prettier and Eslint.

## Prettier

Prettier is an opinionated code formatter.

https://prettier.io/

#### Install prettier

```bash
$ npm install --save-dev --save-exact prettier
```

#### Options

https://prettier.io/docs/en/options

#### Example prettier script on package.json

```json
{
  "scripts": {
    "prettier:check": "prettier --check .",
    "prettier:format": "prettier --write ."
  }
}
```

#### Example prettier config

```json
{
  "prettier": {
    "printWidth": 80,
    "tabWidth": 2,
    "useTabs": false,
    "semi": true,
    "singleQuote": true,
    "trailingComma": "all"
  }
}
```

#### Example prettier ignore file

.prettierignore

By default ignore node_modules

```
dist
package-lock.json
```

## Eslint

Eslint is a static code analysis tool for identifying problematic patterns found in JavaScript code.

https://eslint.org/

#### Install eslint

```bash
$ npm install --save-dev eslint
```

#### Initialize eslint config file

```bash
$ npx eslint --init
```

#### Rules:

https://eslint.org/docs/latest/rules/
https://typescript-eslint.io/rules/
https://standardjs.com/rules

```bash
$ npm install --save-dev eslint-plugin-prettier
```

More details:
https://github.com/prettier/eslint-plugin-prettier

Avoid that prettier and eslint rules conflict

```bash
$ npm install --save-dev eslint-config-prettier
```

More details:
https://github.com/prettier/eslint-config-prettier

#### Example eslint script on package.json

```json
{
  "scripts": {
    "lint": "eslint \"{src,apps,libs,test}/**/*.ts\" --quiet --fix"
  }
}
```

#### Example eslint config

```json
{
  "parser": "@typescript-eslint/parser",
  "extends": [
    "plugin:@typescript-eslint/recommended",
    "plugin:prettier/recommended"
  ],
  "parserOptions": {
    "ecmaVersion": "latest",
    "sourceType": "module"
  },
  "rules": {
    "eqeqeq": ["error", "always"],
    "no-empty-function": "error",
    "no-implicit-coercion": "error",
    "@typescript-eslint/no-explicit-any": "error",
    "@typescript-eslint/no-duplicate-enum-values": "error",
    "@typescript-eslint/no-inferrable-types": "off"
  }
}
```

#### Example eslint ignore file

.eslintignore

```
package.json
package-lock.json
dist
```

### Examples

https://github.com/colbyfayock/my-husky-project/tree/main%2Btest
https://github.com/pedrovelasquez9/react-typescript-eslint-prettier-husky-template

## Husky

https://git-scm.com/docs/githooks

https://github.com/typicode/husky

#### Installation

The next installation was used in husky with package.json

```bash
$ npm install husky --save-dev
```

```bash
$ yarn add husky -D
```

To create a .husky folder and add the pre-commit file

```bash
$ npx hunsky-init && npm install
```

#### Define a script in package.json. (Alternative installation)

1. Install Husky using the npm package manager.
2. Create a .husky directory in the project root.

```bash
$ npm set-script prepare 'husky install'
$ npm run prepare
```

3. Create a pre-commit hook in the .husky directory. This hook will run the npm run lint command before each commit.

```bash
$ echo "npx lint-staged" > .husky/pre-commit
$ echo "npm test" > .husky/pre-commit
```



#### Add hooks in package.json instead of using npx husky add

```json
{
  "husky": {
    "hooks": {
      "pre-commit": "npm run prettier:format && git add -A ."
    }
  }
}
```

### Lint-staged

https://github.com/okonet/lint-staged

```bash
$ npm install --save-dev lint-staged
```

#### Exampe .lintstagedrc config file

```json
{
  "*.{js,jsx,ts,tsx}": ["eslint --fix", "git add"]
}
```

#### Example using script command in package.json

```json
"lint-staged": {
    "*.{js, jsx,ts,tsx}": [
      "eslint --quiet --fix"
    ],
    "*.{json,js,ts,jsx,tsx,html}": [
      "prettier --write --ignore-unknown"
    ]
  },
```

More details:
https://dev.to/shashwatnautiyal/complete-guide-to-eslint-prettier-husky-and-lint-staged-fh9
https://carlosazaustre.es/husky-lintstaged
