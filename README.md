# @stackr23/styleobjects-loader
> **load StyleSheets as JS-Objects** (webpack-loader)

[![Build Status](https://travis-ci.com/stackr23/styleobjects-loader.svg?branch=master)](https://travis-ci.com/stackr23/styleobjects-loader)
[![npm version](https://badge.fury.io/js/%40stackr23%2Fstyleobjects-loader.svg)](https://badge.fury.io/js/%40stackr23%2Fstyleobjects-loader)
[![devDependencies Status](https://david-dm.org/stackr23/styleobjects-loader/dev-status.svg)](https://david-dm.org/stackr23/styleobjects-loader?type=dev)
[![Known Vulnerabilities](https://snyk.io/test/github/stackr23/styleobjects-loader/badge.svg)](https://snyk.io/test/github/stackr23/styleobjects-loader)<br />
[![Maintenance][maintenance-img]][maintenance-url]
[![PRs Welcome][pr-welcome]](http://makeapullrequest.com)

[maintenance-img]: https://img.shields.io/badge/Maintained%3F-yes-green.svg
[maintenance-url]: https://GitHub.com/stackR23/styleobjects-loader/graphs/commit-activity
[pr-welcome]: https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat-square

### v1 roadmap  
* [x] inject style's subclasses recursively  
* [ ] use "@stackr23/styleobjects" instead of nativeCSS  
* [ ] use [humps](https://www.npmjs.com/package/humps) for objectKeys  
* [ ] testscripts, DocBlocks, Comments  
* [ ] ES6 (/dist + buildScript)

## v0.5.0 released  
> __stable version with webpack 4 compatibility__  

### what is it?
* webpack loader
* per [nativeCss](https://github.com/raphamorim/native-css)
* transforms css-properties to camelCase
* very handy for react style injections

### how to use it? 
```npm install @stackr23/styleobjects-loader --save-dev```

__your.so__
```Stylus
.test
	font-size 20px
#anotherTest
	padding-top 5px
.test23
	font-size 23px
    .testInner
        font-decoration none
```

__your.js__
```Javascript
let style 	= require('@stackr23/styleobjects-loader!stylus-loader!./your.so');

console.log(style);
// {
// 	test: {
// 		'fontSize': '20px'
// 	},
// 	anotherTest: {
// 		'paddingTop': '5px'
// 	},
// 	test23: {
// 		'fontSize': '23px'
//      testInner: { // atm: only 1 lvl deep
//          'fontDecoration': 'none'
//      }
// 	}
// }
```

__what else to know?__
> to __keep the style properties__ as they are, pass the query 'transform=false' to the loader  
```Javascript
let style = require('@stackr23/styleobjects-loader?transform=false!stylus-loader!./your.so');
```

> for __pure css__ just use
```Javascript
let style = require('@stackr23/styleobjects-loader!./your.css');
```

> for __other style preprocessor__ syntax (less, sass, scss, ...)
> just add the realated loader (the loader has to output css!)
```Javascript
let style = require('@stackr23/styleobjects-loader!sass-loader!./your.sass');
```

> for ES6/7 usage, __define loaders in the webpack config__  
```Javascript
{
    test: /\.(so)$/, // .so = custom file extension
    loader: '@stackr23/styleobjects-loader?transform=true!stylus-loader'
}
// so you can just
// import yourStyleObject from '/styles/your.so'
```

### issues
* for objectformat and enhanced usage go to [nativeCss](https://github.com/raphamorim/native-css)
* loader related issues or PR's are welcome
* __known issues__: 
    * native-css not found (issue #18)
