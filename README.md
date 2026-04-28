# Introduction to Node.js

Node.js is a JavaScript runtime that runs on Chrome's V8 JavaScript engine. Node.js was developed and invented in 2009 by Ryan Dhall.
At first, its name was web.js, but after realizing its potential, Ryan named it Node.js
There is a big contribution by a company named **Joyent**. This company was building something similar to Node.js, and after seeing Ryan's project, they hired Ryan and funded Node.js.
Node.js follows an event-driven architecture.
Back in days Apache HTTP Servers were popuplar and they were blocking servers, Node.JS came up to solve this blocking problem
**Node.js is non-blocking**
Node.js is managed and maintained by OpenJS foundation


# Lets wrirte code
After installing node in our local machine the command enables few feature which we can use in terminal.
by time **node -v** will give you the node version and by typing **npm -v** will give you the npm version
`Note: When we install node js it installs the npm by default`

**Node REPL (Read, Evaluate, Print, Loop)**

It means when you type node in terminal it gives a run time where you can write javascript code and it will be execuated. Behind the scene it runs the v8 engine. It is similar to the browser console.
Node REPL is only there to execuate some testing code obviously we cannot write whole program in the terminal.
we can create a file app.js in local computer and write a javascript code in it and to run it with node we can simply type `node app.js` and it will simply execute the code.

**Global object in Node**

Lets talk about global object in node js, We have sceen that in borwser if we type `window` it gives us the global object or if we type `this` it points to the same object
but in node it is differet. in Node we have pointer `global` which points to the global object.
> Note: typing `this` in node js shows the empty object it means that this does not points to the global object as we have sceen in browser javascript.  

**GlobalThis**

It was introduced ECMAScript 2020 where writing `globalThis` will points to the global object no matter what the enviroment is. In browser it will points to the window and in node run time it will point to the global object.


**module.exports & require**

Now we all understand that writing a code in a single file is frustrating. We always need to split our code into multiple files and all of the file needs to work togather at the end.
These are called modules in node js. Lets create a file called `sum.js` in some.js we will simple log something.

`sum.js`
```
console.log('hello')
```

Now to import it in our app.js file we need a funtion that is called **require()** this function takes a path of the file.
in app.js we simpply write like this:

```
require('./sum');

const a = 'Test'
console.log(a);
```

now the output will be something like this

```
hello
Test
```

Now lets div deep and try to create a function function in sum.js which will sum 2 values and print it into the console and we will try to call this function in app.js

sum.js
```
function sum(a,b){
console.log(a+b);
}
```

app.js
```
sum(2,4);
```

Will this work? **No** this will not work because the member of a module (variables, functions) are private by default to that module we cannot directly call it into any file 
unless the module wants to. To call this function we have to first export it and import it into app.js. By doing so we will be able to call it then.
To export and import the method there are few steps that we need to follow. To export we have to write a object that is called **module.exports**
mode.exports refers to an object.
> Note: when we require some file into our module behind the scene nodejs wraps all of the module's code into a IIFE (immediately invoked function expression) and then execute it. That is why it has the private scope. Module private system works as the same way as function in javascript.

sum.js
```
function sum(a,b){
console.log(a+b);
}

module.exports = sum;
```

app.js
```
const obj = require('./sum');

obj.sum(2,4);
```

Now this code will show an output in console `6`. We can also destructure it on the fly like `const {sum} = require('./sum');` so we dont have to type `obj` everywhere in the file.
Now for example there are multiple methods we have in sum.js file and we want to export it. How we can do that?
Lets take a look on example below:

sum.js
```
function anotherSum(c,d){
console.log(c+d);
}

function sum(a,b){
console.log(a+b);
}

module.exports = {
sum,
anotherSum
};
```

This example shows that we can assign a object to modeule.exports and export methods and variables more than one and to import we simply need to type `const {sum, anotherSum} = require('./sum');`
>Note: This is a default pattern of importing and exporting modules and variable in node.js

**What happen when we require some module ?**

```
require('./xyz.js')
```
Behind the scene this require function first resolve the file type weather its local file `./` or its a node module `require(node:somemodule)` or it is a json file `./some.json`
Then it will load the module's code according to file type and after loading it will wrap the content into a IIFE `(function(){}())` after wrapping it will evaluate the file and inject the module paramter into IIFE and at the end it will cache the file's content.

Resolving the file --> Loading the module's content according to file type --> wraps it inside IIFE --> Injects `module` parameter --> Caching.


**CommonJS and ES Modules**

We have 2 modules system available in node js first is commonJS refers as `cjs` and second is Es Module refers as `mjs`. They both have some differences.
There are 2 major difference that we need to know is that common js module system is synchronouse and ES modules systems ia asynchronouse it means that in synchronouse next line will be executed only after module is fully loaded.
```
require('somefile')
const a = 1;
```
it means that variable a will only be executed and run after  code in `somefile` will fully be loaded.
The 2nd major thing is **Strict Mode** Common JS modules system runs in non-strict mode and ES Module system runs in Strict mode. Lets take a look to an example below:

```
const a = 'Zain'
b = 'Thi will not show an error while running'
```
In non-strict mode or common JS module system the code will be executed and it will not show an error.
> Note: CommonJS module system is an older way if importing and exporting and it is widely used in projects.

Lets talk about **ES Modules** system. It is not the default and we have to enable it to use it in our project. To do that first we need to create a `package.json` file
package.json
```
{
"type": "module"
}
```
in package.json file we have to wirte type: module to use the ES module system. 
In ES module we have a different way of exporting and importing the file as compare to commonJs module system. Lets take a look to an example below:

sum.js
```
export let a = 1;
export somefunction() {
// some code
}
```
app.js
```
import {a, somefunction} from './sum'

// some code
```

This is how we export and import the module in mjs or known as ES module. This module system is by default followed by lots of Frontend libraries like react, next, angular and vue.
ES modules load modules asynchronously, allowing for more efficient and flexible code execution. This distinction is a powerful feature.

The second major difference is Strict mode in `mjs`. It means that if we try to execute the code we have written above
```
const a = 'Zain'
b = 'Thi will   show an error while running'
```
it will throw an error. It makes the module generally safer than the older way which is commonjs.

# Libuv & Async I/O

Nodejs basically a wrapper which wraps v8 engine and libuv library to handle syncronous and asyncrounous task, for simple syncronous task v8 engine executes them directly without any problem but for async task like reading the file from your OS, making an api call or talking to the timer in your OS v8 engine just simply ofloads it to libuv and libuv handles them.
Basically libuv act as a middle layer between v8 engine and async I/O tasks. Node js is asyncronous because of libuv.
> Note: Libuv is a open source library which is written in C




































































































































