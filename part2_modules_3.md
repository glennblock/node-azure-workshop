# node-uuid 
Generates UUIDs in javascript (https://github.com/broofa/node-uuid)

```javascript
var uuid = require('node-uuid');
console.log(uuid.v4());
```

# request
A module for simplifying HTTP requests (https://github.com/mikeal/request)

Below is a simple request that involves a redirect
```javascript
var request = require('request');
request('http://www.nodejs.org/api', function (error, response, body) {
  if (!error && response.statusCode == 200) {
    console.log(body) // Print the node api page
  }
})
```

* is much more terse
* follows redirects

request can easily pipe the response to file.

```javascript
var request = require('request');
request('http://google.com/doodle.png').pipe(fs.createWriteStream('doodle.png'))
```

request can handle sending multipart content

```javascript
var request = require('request')
, rand = Math.floor(Math.random()*100000000).toString();

request(
  { method: 'PUT'
  , uri: 'http://mikeal.iriscouch.com/testjs/' + rand
  , multipart: 
    [ { 'content-type': 'application/json'
      ,  body: JSON.stringify({foo: 'bar', _attachments: {'message.txt': {follows: true, length: 18, 'content_type': 'text/plain' }}})
      }
    , { body: 'I am an attachment' }
    ] 
  }
, function (error, response, body) {
    if(response.statusCode == 201){
      console.log('document saved as: http://mikeal.iriscouch.com/testjs/'+ rand)
    } else {
      console.log('error: '+ response.statusCode)
      console.log(body)
    }
  }
 );
```
# express
express is a Sinatra inspired web framework (http://expressjs.com/guide.html)

Below is an express hello word

```javascript
var express = require('express');
var app = express();

app.get('/hello.txt', function(req, res){
  res.send('Hello World');
});

app.listen(3000);
console.log('Listening on port 3000');
```

* app.get - specifies a route to listen to and an associated handler.
* res.send - used for sending JSON objects or strings.

# socket.io
socket.io is a real time framework for bi-directional communication (http://socket.io)

server.js
```javascript
var io = require('socket.io');

io.sockets.on('connection', function (socket) {
  console.log('connected');
  setTimeout(function() {
    socket.emit('greeting', { message: 'Welcome to socketio.on Windows Azure' });
    socket.on('login', function (data) { 
      console.log('Logged in user:' + data.user + ' password:' + data.password);
      setTimeout(function() {
        socket.emit('message', {message: 'Hello ' + data.user});
      },300);
    });
  }, 300);
});

* socket.emit - sends a message to the client
* socket.on - subscribe to specific events from the client
* sockets.on - subscribe to general events
```

index.jade
```text
doctype 5
html
  head
    script(src='/socket.io/socket.io.js')
    script(src='http://code.jquery.com/jquery.min.js')
    script
      var socket = io.connect();
      
      socket.on('greeting', function (data) {
        $('#greeting').append(data.message + '<br>'); 
        $('#activity').append("Logging in as 'User'<br>");
        socket.emit('login', { user: 'User', password: 'pa$$w0rd' });
      });

      socket.on('message', function(data) {
        $('#activity').append(data.message + '<br>'); 
      });
  #greeting
  hr
  #activity
```

* socket.emit - sends a message to the server
* socket.on - subscribe to messages coming from the server



