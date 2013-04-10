# REPL
node has a repl.

```text
node
> console.log('Hello from node');
Hello from node
undefined
>
```

# Hello World

```javascript
var http = require('http');
http.createServer(function(req,res) {
  res.writeHead(200, {'Content-Type': 'text/plain'});
  res.end('Hello QCon\n');
}).listen(3000);
console.log('Listening on port 3000');
```
### json everywhere
Most APIs accept simple JSON objects, no base class necessary :-)

### require - used to load modules. More [here](http://nodejs.org/api/)
Core modules are built in.
  * http/https: HTTP(s) server and clients
  * net: TCP servers and clients
  * fs: File I/O
  * child_process: spawn and manage child processes
  * globals: console, process args, env variables.

### http.createServer([requestListener])
Creates an [HTTP server] (http://nodejs.org/api/http.html#http_class_http_server). Takes a function(req,res) which will be invoked on each request.
* _req, res_ - HTTP request/response object. 
* _res.writeHead_ - Write all HTTP headers
* _res.end_ - Write to the body and end.

### server.listen(port)
Listen on a port. 
* port can be either a port number or a named pipe

# Callbacks
* node is designed for writing non-blocking code.
* 95% of APIs in node are async accepting a callback.
* The general convention is the first parameter of the callback is an err object. It will be null / undefined if there is no error
e.g:

  ```javascript
  fs.fstat(fd, function(err, stats) {…}
  ```

* Some methods violate this convention like createServer and path.exists e.g.

  ```javascript
  path.exists (p, function(exists)) {…}
  ```

## Nesting vs flattening
* Due to node's async nature, it is very common to chain callbacks together.
* If you nest anonymous callbacks code will get very ugly and hard to maintain such as this:

```javascript
DoSomething(function(err, result) {
  DoAnotherThing(function(err, result) {
    DoEvenAnotherThing(function(err,result) {
      exit();
    });
  });
});

function exit() {
  //...
}
```

* Instead consider refactoring to named functions and pass those functions as the callback. This provides the added benefit of 

```javascript
function DidSomething(err, result) {
  DoAnotherThing(DidAnotherThing);
}

function DidAnotherThing(err,result) {
  DoEventAnotherThing(DidEvenAnotherThing)
}

function DidEvenAnotherThing(err, result) {
  //exit
}

DoSomething(DidSomething);
```

* Or nest related functions as inner functions

```javascript
function ExecuteDoSomething(callback) {
  function DidSomething(err, result) {
    DoAnotherThing(DidAnotherThing);
  }

  function DidAnotherThing(err,result) {
    DoEventAnotherThing(DidEvenAnotherThing)
  }

  function DidEvenAnotherThing(err, result) {
    callback();
  }

  DoSomething(DidSomething);
}

```

* This provides an adding scoping benefit for example the callback variable above.
* There are some helpers for making async code easier to manage such as the async module which will be covered later.

