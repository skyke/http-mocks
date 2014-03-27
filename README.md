## http-mocks

http-mocks is a mocking library for for [Node.js](http://nodejs.org/) inspired
by [node-mocks-http](https://github.com/howardabrams/node-mocks-http) by Howard Abrams.
I revised/refurbished some parts of his library to better suit the needs of my current projects.

So for the full documentation please see his [github account](https://github.com/howardabrams/node-mocks-http).

## Issues with node-mocks.http

1. EventEmitter was not triggered whenever you perform `end` on the response.
 ```javascript
 var httpMocks = require('http-mocks');
 var EventEmitter = require('events').EventEmitter;

 var req = httpMocks.createRequest();
 var res  = httpMocks.createResponse({
                 eventEmitter: EventEmitter
             });

 res.on('end', function() {
  // Do your magic
 });

 res.end('Hello there!!');
 ```

2. The response did not have a body property, whenever you wanted to check the content you
  needed to execute `_getdata()`. It's a minor thing but if you use express you can also get the content via the `body`
  property.

3. No content negotiation. When you set the header `content-type` as `application/json` you should expect a json object
whenever you fetch the body of the response.

Old fashion:
```javascript
// If data is empty JSON.parse() will throw an exception :(
var data = response._getData();
var json = null;
if(data) {
  json = JSON.parse(data);
} else {
  json = {};
}
```

New method:
```javascript
var json = response.body;
```



## Installation

This project is available as a NPM package.

    npm install http-mocks

