# express-sanitized

[![Build Status](https://travis-ci.org/fingerfoodstudios/express-sanitize-escape.svg?branch=master)](https://travis-ci.org/fingerfoodstudios/express-sanitize-escape)

## Installation

```
npm install express-sanitize-middleware
```

## Usage

Place this directly after all express.use(bodyParser) middlewares and before any express middleware that accesses query or body parameters, e.g.:


```javascript
var bodyParser = require('body-parser');
var express = require('express');
var expressSanitized = require('express-sanitize-escape');

app.use(bodyParser.urlencoded);
app.use(bodyParser.json);
app.use(expressSanitized()); // this line follows app.use(bodyParser.json) or the last body parser middleware

```


## Output

The string 
```javascript
'<script>document.write('cookie monster')</script> download now'
```
will be sanitized to ' download now'.

and 
```javascript
'< > ' " &'
```
will be escaped to `&lt; &gt; &#39; &quot; &amp;`

## Limitations

This is a basic implementation of [Caja-HTML-Sanitizer](https://github.com/theSmaw/Caja-HTML-Sanitizer) with the specific purpose of mitigating against persistent XSS risks. 
And [node-htmlencode](https://github.com/danmactough/node-htmlencode) to escape all html entities

## Caveats

This module trusts the dependencies to provide basic persistent XSS risk mitigation. A user of this package should review all packages and make their own decision on security and fitness for purpose. 

This module was inspired by [express-sanitizer](https://www.npmjs.org/package/express-sanitizer) and [express-sanitized](https://www.npmjs.org/package/express-sanitized).
  The difference here is:
  This middleware automatically sanitizes post and query values parameter.
  And automatically html escapes all strings.

## Changelog

### v0.6.1
- Added additional test for nested object and an array 
- Added chai js for testing

### v0.6.0
- Added htmlencoding
- Change filer to recurse through all values of the object and sanitize only values that are strings
- Updated docs to express 4.x and new bodyParser middleware
- Added License file

### v0.5.1
- Initial release

## Contributors

- Patrick Hogan <patrick@callinize.com> - Wrap the sanitizer in an npm package
- Mark Andrews <20metresbelow@gmail.com>* - Wrote the initial express-sanitizer.  I forked his library.
- [Callinize](http://www.callinize.com)

## License

Copyright (c) 2016 Finger Food Studios <justin@fingerfoodstudios.com>, MIT License

