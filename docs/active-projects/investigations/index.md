# Formal Education Investigations

## Introduction

The investigations explore Astronomy 101 topics through an interactive question-answer format using LSST data. The investigations are currently being built as static-sites that rely on locally loaded precursor data (NOT LSST data). This section describes the current investigation work flow and stack.

## Work Flow

Developers collaborate with designers and members of the Education Team to design, build, and test the investigations. Educational materials (Teacher's guides, notebooks, and links to supplemental documentation) can be found in the GOAT Google Doc. Developers and designers work from these materials (and directly with other team members) to create the investigation web apps. 

Currently the apps are:

* Consuming precursor data as JSON
* Designed in [Sketch](https://www.sketch.com/)
* Coded in ES6 Javascript, [React](https://reactjs.org/docs/getting-started.html), SCSS, and HTML
* Built using [Webpack 4](https://webpack.js.org/)
* Deployed as a static site to Github Pages (for production) and [Netlify](https://www.netlify.com/)(for staging)

## The Stack

### Data

The investigation app consumes JSON for precursor astronomical data:

* [Example data format](stellar-data-example.md)
* [Example local http request](axios-request-example.md) using [Axios](https://github.com/axios/axios)

### ES6 Javascript

Modern JS is transcompiled to vanilla javascript using babel. Important ES6 functionality includes:

* `import NodeModuleName from 'NodeModuleName'` [Imports](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import). The glue that points every piece of your web app and every other piece or external dependency. Also helps webpack to make good choices during its builds.
* `class` [Classes](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes). A more concise, legible, and fancier alternative to the vanilla [prototypical inheritance](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Inheritance_and_the_prototype_chain#Using_prototypes_in_JavaScript). 
* `=>` [The fat arrow](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions). When writing a `class` fat arrows can help in managing what `this` is.
* `[..1, 2, 3]` [The spread operator](https://codeburst.io/javascript-es6-the-spread-syntax-f5c35525f754). Particularly helpful when [[managing React state|react-state-management]]
* [Destructuring objects](https://wesbos.com/destructuring-objects/). Particularly useful in React when taking apart props for use in a Component function, or in the render method.
* `@decoratorName` [Decorators](https://www.sitepoint.com/javascript-decorators-what-they-are/). A pattern popular in some React libraries.
* `beginnging-string${variableName}end-string` [String Interpolation](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals)
