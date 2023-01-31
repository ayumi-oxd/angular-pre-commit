# Angular with pre-commit hooks

This project was generated with [Angular CLI](https://github.com/angular/angular-cli) version 15.1.3.

## Setup husky pre-commit hooks

1. Install [husky](https://typicode.github.io/husky) and [lint-staged](https://github.com/okonet/lint-staged)
```
yarn add -D husky lint-staged
```

2. Setup husky
```
npx husky-init
```

3. Go to `.husky/pre-commit` and edit the file:
```
#!/usr/bin/env sh
. "$(dirname -- "$0")/_/husky.sh"

# npm test
npm run lint-staged
```

4. Go to `package.json` and edit the file:
```
"scripts": {
    "lint-staged": "lint-staged"
},
```
```
"husky": {
    "hooks": {
        "pre-commit": "lint-staged",
        "pre-push": "npm run lint"
    }
},
"lint-staged": {
    "**/*.{tsx,ts}": [
        "prettier --write",
        "eslint \"{src,apps,libs,test}/**/*.ts\" --fix"
    ]
}
```

## Usage

1. Stage your un-committed files
```
git add .
```

2. Commit your change
```
git commit -m <commit message>
```
`lint-stage` will run to lint the files. If there is any linting issue, it will not proceed to commit the files, else, the staged files will be formatted automatically and committed.

3. Push your changes to repo
```
git push
```