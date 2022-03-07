[PostCSS](https://github.com/postcss/postcss) is a transpiler/linter for CSS and CSS like languages.  With it you can use bleeding-edge CSS properties and standards, but mostly we use it to get [Autoprefixer](https://github.com/postcss/autoprefixer) into the mix.  

Autoprefixer is absolutely, 100%, indispensable.  It injects all of those vendor prefixes you never remember, making cross-browser support just that much easier. Thank you Autoprefixer.

PostCSS Config lives in the root of your project and is named `.postcss.config.js`

```js
module.exports = {
  plugins: [
    [
      "postcss-preset-env",
      {
        autoprefixer: {
          flexbox: "no-2009",
          grid: false,
        },
        stage: 2,
      },
    ],
    [
      "postcss-normalize",
      {
        forceImport: true,
      },
    ],
  ],
};

```