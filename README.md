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

It means when you time node in terminal it gives a run time where you can write javascript code and it will be execuated. Behind the scene it runs the v8 engine. It is similar to the browser console.
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
















