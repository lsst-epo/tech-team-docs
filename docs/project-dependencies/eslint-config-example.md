[ESlint](https://eslint.org/) configs and ignore files live in the root of your project and are named `.eslintrc` and `.eslintignore` respectively.

A config based on the popular [Airbnb config](https://github.com/airbnb/javascript) and prettier's recommended formatting, that uses babel, might look like:

```js
require("@rushstack/eslint-patch/modern-module-resolution");

module.exports = {
  root: true,
  env: {
    browser: true,
  },
  rules: {
    // let next/link package handle anchor attributes
    "jsx-a11y/anchor-is-valid": 0,
    // next/link handles the href, so anchors without href are still interactive
    "jsx-a11y/no-noninteractive-tabindex": ["error", { tags: ["a"] }],
    // throwing false negatives on components using Atomics.Image
    "jsx-a11y/alt-text": 0,
    // storybook stories are exported this way
    "import/no-anonymous-default-export": 0,
    // would be good to use next/image but we aren't yet
    "@next/next/no-img-element": 0,
  },
  extends: ["@castiron", "next"],
};

```

A basic ignore file for a project with tests, built assets, and webpack, might look like:

```
.next/*
node_modules
out/*
```