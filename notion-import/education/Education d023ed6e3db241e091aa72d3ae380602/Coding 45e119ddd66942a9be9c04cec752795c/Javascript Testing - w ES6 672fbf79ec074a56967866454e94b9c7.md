# Javascript Testing - w/ ES6

Last Edited: December 19, 2019 11:43 PM

Need Dependencies:

- yarn add -D babel babel-polyfill
- [if node] yarn add -D babel-register
- [presets] yarn add -D babel-preset-es2015 babel-preset-react

Root files:

[.babelrc]

{

"presets": ["es2015", "react”]

}

**Browserify users** should install the babelify transform library. This allows Browserify to transform the code using Babel during the bundling process.

- yarn add -D babelify

Add to package.json

"browserify": {

"transform": ["babelify”]

}