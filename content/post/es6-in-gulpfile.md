---
date: 2015-04-26
title: "Use ES6 in Gulpfile.js"
slug: "use-es6-in-gulpfile-js"
tags: [ "es6", "node", "gulp" ]
categories: [ "development" ]
---

[Gulp](http://gulpjs.com/) doesn't natively support Ecma Script 6 (ES6), so in order to get it working we need to first transpile our `gulpfile.js` file before it can be read by gulp.

A clean way of acheiving this is to have the default gulp file `gulpfile.js` that acts as a shim to load and transpile the ES6 version (in my case `gulfile.es6.js`).

[Babel](https://babeljs.io/) has a neat hook into `npm` that allows us to automatically transpile `required` statements on the fly. To install simply add the package:

```bash
npm install babel --save-dev
```

#### Gulpfile.js

```javascript
require('babel/register');
require('./gulpfile.es6.js');
```

The `require('babel/register')` statement above is the [hook](https://babeljs.io/docs/usage/require/) that makes all of this possible.

#### Gulpfile.es6.js

```javascript
import gulp from 'gulp';

// uses ES6 lambda
gulp.task('hello', () => { console.log('hello'); });

gulp.task('default', ['hello']);
```

You can find the [full example](https://github.com/sandcastle/example-es6-gulp) on GitHub that shows the use of external files, generators and classes.
