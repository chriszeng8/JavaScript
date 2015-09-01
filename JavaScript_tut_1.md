##Global Object
Two things that can be really handy:

1. Developer Tool within browser (Chrome: top right -> More Tools -> Developer Tools)
2. Bracket io editor

###this/window object
this = window

Go to developer tool -》 switch to "Console" tab, we can debug here: try entering "this" and "window" and see what the outcome is

###global
global = not inside a function

##Hoisting
The variable/functions exists before your code is executed line by line: Before your code is executed line by line, JavaScript set up memory space for variables and functions (before) fully allocate values to variable or definitions to function.

```javascript
b();
console.log(a);

var a = 'Hello World!';

function b() {
    console.log('Called b!');
}
```
The console gives log output:
```javascript
Called b!
app.js:2 undefined
```

We can see that the function (without input arguments) got executed regardless of where it is defined in the code. However, function with assignment as input is undefined (however, this is not throwing an error, it is just return undefined as output). In short, all variables are set as undefined initially before code got executed line by line.

####Undefined (value not allocated yet) != not defined (error)
When declare variable without assigning value to it, this is undefined variable (meaning the value of this variable is not allocated/undefined).  However, if variable is never declared but used as argument in other functions. This will throw an error complaining such variable itself is not defined.

```javascript
var a;
console.log(a)
```
returns ``undefined`` in console, whereas

```javascript
console.log(a)
```
returns ``Uncaught ReferenceError: a is not defined``

Think ``undefined`` as a value for a variable, in fact, it is a special value for any variable, and one can set a variable as ``undefined``:
```javascript
a = undefined
```