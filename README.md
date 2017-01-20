# add-stream [![Build Status](https://travis-ci.org/wilsonjackson/add-stream.svg?branch=master)](https://travis-ci.org/wilsonjackson/add-stream)

> Append the contents of one stream onto another.

## Usage

```js
var fs = require('fs');
var es = require('event-stream');
var addStream = require('add-stream');

// Append strings/buffers
fs.createReadStream('1.txt') // 1.txt contains: number1
	.pipe(addStream(fs.createReadStream('2.txt'))) // 2.txt contains: number2
	.pipe(fs.createWriteStream('appended.txt')); // appended.txt contains: number1number2

// Append object streams
es.readArray([1, 2, 3])
	.pipe(addStream.obj(es.readArray([4, 5, 6])))
	.pipe(es.writeArray(function (err, array) {
		console.log(array); // [ 1, 2, 3, 4, 5, 6 ]
	}));
```

## API

### var transformStream = addStream(stream, opts = {})

Create a transform stream that appends the contents of `stream` onto whatever
is piped into it. Options are passed to the transform stream's constructor.

### var transformStream = addStream.obj(stream, opts = {})

A convenient shortcut for `addStream(stream, {objectMode: true})`.

## License

MIT

Copyright (c) 2017 Majid Burney

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
