# Project Dependencies

All of the following project level dependencies are Node packages (modules).  There are three main categories: packages useful in your IDE, packages useful in development (not included in the build), packages useful in production (included in the build).

## In the IDE

These packages will be installed globally.  You can use `npm` or `yarn`.  

Most of these tools aim to keep a codebase uniform across contributors, as well as organized and legible.  Mostly these tools enforce opinions about the format and structure of the code on the page.

All of the tools in this section can be configured to produce `errors` or `warnings`, and in turn halt builds or commits, or just print infractions and suggestions in the terminal. They can be configured to fix problems automatically. You can also use them in conjunction with IDE plugins in order to view and fix rule infractions in-place. Rules and tools can be disabled inline, or for an entire file.

### editorconfig

[EditorConfig](https://editorconfig.org/) is a code styling tool.  Code styling impacts the basic level of formatting different code (file types) in your IDE.  For instance controlling indentation/spacing. It is not concerned with how you are using the languages corresponding to the designated file types.  This configuration will only have an effect if you add the [corresponding plugin](https://editorconfig.org/#download) to your IDE.  The config is a `.editorconfig` file in the project root of the project.

[Example config](editor-config-example.md)

### prettier

[Prettier](https://prettier.io/) is an opinionated code formatter that works with many popular languages, including js, jsx, scss, and ruby. For the most part, on our projects, we only use it for js and jsx, and its use is knit into how we use [ESLint](https://eslint.org/): ESlint manages any/all linters that interact with javascript-like files, Prettier included, and Prettier is responsible for the "structure" of those files, while other linters/configs handle how the javascript in those files is implemented.  For instance, we might use prettier to control when and where commas or line breaks are included, but we would use another linter to decide when a variable should be defined using `let` vs `const`.  Prettier should be configured in the `.eslintrc` file but it can also be configured in its own `.prettierrc` file.

### eslint

[ESLint](https://eslint.org/) is a js and jsx linter that helps you to follow ES6/Javascript best practices, adopt popular patterns and adhere to style guidelines. Being such a flexible and loosely-typed language, Javascript is especially prone to developer errors that can not be spotted until you execute the code.  Dutifully linting your code can help you avoid some of the more common syntactical errors, and also ensure your code conforms to standards other developers might be familiar with (and hopefully increase legibility). One such standard we rely on is [Airbnb's styleguide](https://github.com/airbnb/javascript).

[Example config](eslint-config-example.md)

### stylelint

[StyleLint](https://stylelint.io) is for styles (CSS, SCSS, Sass, or Less) what ESLint is for Javascript.  With it you can enforce rules about general formatting, what properties are allowed, and catch syntactical errors.  For instance we use stylelint to enforce rules about the order properties should be in, how many levels of nesting are allowed, and what formats for colors are allowed (hex vs rgb vs color name).

[Example config](stylelint-config-example.md)

## In Development

### webpack

[Webpack](https://webpack.js.org/) is a dev tool used to build and bundle assets.  In our work these assets primarily take the form of styles, Javascript, precursor data, and any typography, images, and icons served locally.  How to create a webpack config is well out of the scope of this documentation. However, it is important to note that Webpack, in essence, is just a tool for telling other tools what to do.  Therefore the configs and set up of the various plugins Webpack interacts with is crucial to a project successfully building assets in the manner you expect.  

In our work we typically adopt frontend React Frameworks that make use of Webpack under the hood, but present their own means of configuring stuff that's like one step removed from Webpack itself.

## browserslist

Like Webpack, [browserslist](https://github.com/browserslist/browserslist) is a package meant to support the work other packages do.  It provides the ability to configure what browsers and systems other packages (like postcss, autoprefixer, eslint, etc.) should target for any features, polyfills, or workarounds that might apply.  We recommend including these definitions in the package.json file, however a `.browserslistrc` file in the root of your project can be used.

In our work we generally use the following config to target browsers that are still actively maintained (have official support and have had a new version release in the last 2 years), and whose user base is more than 0.5% of all internet browser users. This is the the default setting for `browserslist`.

```json
  "browserslist": [
    "defaults",
    "not IE 11"
  ],
```

### babel

[Babel](https://babeljs.io/) is a javascript compiler that does all the work of transpiling our fancy javascript (be it ES6, JSX, typescript, or something even more experimental) into normal, everyday js any ol' browser will run (aka those browsers targeted by `browserslist`).  Babel. sweet sweet Babel.  Thank you for the gift of modern javascript.  Babel pulls all this off using lots of special workarounds and polyfills.  Some of these are included in the babel core, some of them are provided by babel in the form of additional packages, and some of them are from third-party providers.  These packages are installed as node modules, and referred to in the babel config found in the `package.json` file.  You may also configure Babel using a `.babelrc` file in the root of your project.

```json
  "babel": {
    "presets": [
      "next/babel"
    ],
    "plugins": [
      [
        "styled-components",
        {
          "ssr": true
        }
      ]
    ]
  },
```

### postcss

[PostCSS](https://github.com/postcss/postcss) a transpiler/linter for CSS and CSS like languages. With it you can use bleeding-edge CSS properties and standards, but mostly we use it to use [Autoprefixer](https://github.com/postcss/autoprefixer).

[Example config](postcss-config-example.md)

### autoprefixer

[Autoprefixer](https://github.com/postcss/autoprefixer) is absolutely, 100%, indispensable. It injects all of those vendor prefixes you never remember, making cross-browser support just that much easier. Thank you Autoprefixer.

## In Production

### react

[React](https://reactjs.org/) is a js framework to lend an MVC type approach to frontend development.  Really this is a whole thing, and even a superficial deep-dive is well outside the scope of this documentation.

### next.js

[Next.js](https://nextjs.org/) is a react framework which excels at building static sites, or sites who deliver a mixture of static and dynamic content/pages.  It has a host of convenience methods and classes and optimizations and opinions on project structure, and it's been working pretty well for us.  We started development in this vein using a similar react framework called [Gatsby](https://www.gatsbyjs.com/).  For real reasons, and chance circumstances, we elected to shift from Gatsby to next.js.  And the best we can say about it is, "We haven't looked back since."  You can find more info about our use of next.js on the frontend, and our stack in general, in the [[CMS Backend + React Frontend Stack section|The Stack]].

### d3

[D3](https://d3js.org/) is a js library that is a popular solution for creating interactive data-driven visualizations. It is not enormously developer friendly, but it is incredibly robust and flexible to most any needs. As such going into more detail here is not gonna happen.