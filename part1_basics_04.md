# Process

### process.env
Accesses environment variables
```javascript
console.log('\nEnvironment');
console.log(process.env);
console.log('\nPath');
console.log(process.env.path);
console.log(process.env['path']);
```
* env is an object which contains properties for each env var, not an array
* env vars can be accessed using a property or using a hash.

### process.argv
Accesses arguments
```javascript
console.log('\nArguments');
process.argv.forEach(function (val, index, array) {
  console.log(index + ': ' + val);
});
```
* argv is an array of arguments
* first argument is always the process that launched the node script
* second argument is the node script
* args are modifiable and can be rewritten

### process.stdin
Accesses the standard input stream
```javascript
process.stdin.resume();
process.stdin.setEncoding('utf8');

process.stdin.on('data', function(text) {
  if (text === '\n')
		process.stdin.pause();
	else
		console.log('entered:' + text);
})
```

* resume: allow keyboard input :-)
* pause: stop accepting input


