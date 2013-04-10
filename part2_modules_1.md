# Modules
node has a very simple module system (http://nodejs.org/api/modules.html). A module is a javascript file which exports functions or objects. modules can reference other modules.

## Authoring a module
Below is an example of a simple module

```javascript
//circle.js
var PI = Math.PI;

exports.area = function (r) {
  return PI * r * r;
};

exports.circumference = function (r) {
  return 2 * PI * r;
};

function creator() {
  return function(message) {
		return {
			foo: message
		} 
	}  
}

exports.creator = creator;
```
* exports is a special object returned from a module
* functions or other objects can be directly attached to the exports object.
* the exports object can also be completely replaced.

The circle module can then be consumed using require.

```javascript
var circle = require('./circle.js');
var Creator = circle.creator();
var creator1 = new Creator('foo1');
var creator2 = new Creator('foo2');

console.log( 'The area of a circle of radius 4 is '
  + circle.area(4));

console.log(creator1.foo);
console.log(creator2.foo);
```

## How modules are resolved?
* If the path is specified wih a relative path it will be loaded directly. 
* If it is not relative, node walks the file system relative to the current path looking for node_modules folders to resolve modules.

Below is the algorithm for resolving non-relative modules. Assume the /root/app/server.js had a require('circle.js'), then node would look in the following folders.

/root/app/node_modules/circle.js <br>
/root/node_modules/circle.js <br>
/node_modules/circle.js <br>

## Side by side versioning
This model allows different modules to be loaded side by side in the same process.

## Module as folders and package.json
By default modules are just loose files however modules can also be folders.

### package.json
When node looks in a module folder it will look in a package.json file if present. This file can specify the main file for the module.

For example the package.json file specifies the module name is circle and the main file to be loaded is /lib/circle.js. 

```javascript
//package.json
{ "name" : "circle",
  "main" : "./lib/circle.js" }
```

thus assuming circle was in /root/app/node_modules/circle/lib then doing require("circle") in /root/app/server.js would load circle.js.

### default
If no package.json is found, then by default node will look for an index.js or index.node in the same folder.



