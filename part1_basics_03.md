# Files
## Writing
```javascript
var fs = require('fs');
fs.writeFile('./file1.txt', 'Some text\n', function(err) {
  if (err) throw err;
  console.log('Wrote file1.txt');
}); 
```

### fs.writeFile(filename, data, [options], callback)
* writes text to a file
* options is a hash specifying addional params like encoding. default is utf8.

## Writing to a stream
```javascript
var fs = require('fs');
var os = fs.createWriteStream('./file2.txt');
os.write('Some text\n');
os.write('Some text\n');
console.log('Wrote file2.txt')
```

### fs.createWriteStream(path, [options]) (http://nodejs.org/api/fs.html#fs_fs_createwritestream_path_options)
* opens a file for streaming and returns a new stream.Writeable

### writable.write(chunk, [encoding], [callback])
* writes a chunk to the stream

## Reading
```javascript
var fs = require('fs');
fs.readFile('./file2.txt', 'utf8', function(err, data) {
  if (err) throw err;
  console.log(data);
});
```

### fs.readFile(filename, [options], callback)
* opens a file for reading and reads all the contents
* the callback is fired once when the reading is completed

## Reading a stream
```javascript
var fs = require('fs');
fs.createReadStream('./file2.txt', {encoding:'utf8',
  bufferSize:5}).
  on('data', function(chunk) {
    console.log('data:' + chunk);
  }).
  on('error', function(err) {
    throw err;
  });
```

### fs.createReadStream(path, [options])
* opens a file for reading and returns a new stream.Readable
* the _data_ event is fired for each chunk that s read.
* _error_ fires for any I/O related errors that occur

# Streams
[Streams](http://nodejs.org/api/stream.html) are used when there is a continuous flow of data in/out.
* A stream is an abstract emitter interface in node that is implemented by various objects like an HTTP Request, Files, Sockets, etc.
* Streams wrap a file descriptor
* node supports both readable and writable streams
* Streams can be piped together
* Pre node 0.10 streams are push, in node 0.10 streams are pull by default.

## Readable streams
### Methods
* pause: pause a stream
* resume: resume a paused stream
* destroy: close the stream
* pipe: pipe all input to another stream

### Events
* data: data has been received
* end: there is no more data
* error: there was an error receiving data
* close: the underlying file descriptor has been closed

## Writeable streams
### Methods
* write: write to a stream
* end: terminate the stream
* destroy: close the stream

###Events
* drain: the buffer is drained
* error: there was an error writing data
* close: the underlying file descriptor has been closed
* pipe: the stream has been piped

## Piping
A readable stream can be piped to a writeable stream.

```javascript
var https = require('https');

req = https.get('https://api.github.com/users/glennblock/repos',onGet); 

function onGet(res) {
  res.pipe(process.stdout);
}

req.on('error', function(e) {
  console.log('problem with request: ' + e.message);
});
```

### process.stdout
Standard output stream for the process

### readable.pipe(destination, [options])
* destination: must be a writeable stream.
* options
  * end: indicates end should be called on the destination stream. Default is true.

## Other things you can do with files
* fs.rename: rename a file
* fs.mkdir: create a directory
* fs.readdir: read the contents of a directory
* fs.stat: get information about a file
* fs.symlink: create a shortcut
* fs.watchFile: monitor file changes

