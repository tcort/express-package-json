# express-package-json

Simple [express](http://expressjs.com/) function to expose the contents
of a `package.json` file to the view engine. This is useful for displaying
the software version on a web page without having to update the page every
time the version changes in `package.json`.

## Installation

    npm install --save express-package-json

## API

### expressPackageJson(pathToPackageJson, propertyName)

Parameters:

* `pathToPackageJson` - path to the `package.json` file. String. Defaults to `./package.json`.
* `propertyName` - name of property to add to `res.locals`. String. Defaults to `pkg`.

Returns:

* express middleware function:
  * middleware function accepts `(req, res, next)`.
  * `res.locals[variableName]` is set to a JavaScript object containing the parsed `package.json`.
  * `next()` is called when complete.

## Example

`app.js`:

    "use strict";

    var express = require('express');
    var expressPackageJson = require('express-package-json');

    var app = express();

    app.set('view engine', 'hbs');    

    app.use(expressPackageJson(path.join(__dirname, 'package.json')));

    app.get('/', function (req, res) {
        res.render('index');
    });

`views/index.hbs`:

    {{pkg.name}} v{{pkg.version}}

## Testing

    npm test

## License

```
Copyright (c) 2015 Thomas Cort <linuxgeek@gmail.com>

Permission to use, copy, modify, and distribute this software for any
purpose with or without fee is hereby granted, provided that the above
copyright notice and this permission notice appear in all copies.

THE SOFTWARE IS PROVIDED "AS IS" AND THE AUTHOR DISCLAIMS ALL WARRANTIES
WITH REGARD TO THIS SOFTWARE INCLUDING ALL IMPLIED WARRANTIES OF
MERCHANTABILITY AND FITNESS. IN NO EVENT SHALL THE AUTHOR BE LIABLE FOR
ANY SPECIAL, DIRECT, INDIRECT, OR CONSEQUENTIAL DAMAGES OR ANY DAMAGES
WHATSOEVER RESULTING FROM LOSS OF USE, DATA OR PROFITS, WHETHER IN AN
ACTION OF CONTRACT, NEGLIGENCE OR OTHER TORTIOUS ACTION, ARISING OUT OF
OR IN CONNECTION WITH THE USE OR PERFORMANCE OF THIS SOFTWARE.
```
