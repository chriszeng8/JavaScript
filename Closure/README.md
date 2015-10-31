###Closure a vital concept in JS
Chris Zeng,  Oct 31, 2015

##W3School's definition:

* A closure is a function having access to the parent scope, even after the parent function has closed (which is a pretty darn good summary). Now we just need additional examples to deepen our understanding.


###Example 1

```
function greet(whattosay) {
   return function(name) {
       console.log(whattosay + ' ' + name);
   }

}

greet('Greetings')('Chris');
// returns "Greetings Chris"
```

The returned output is probably just as you expected. However, there was something unusual happened here (well, unusual for people like me who is from a non-javascript programming background at least). 
Now, imagine we replace the last function call:

```
greet('Greetings')('Chris');
```

with 

```
var SayHi=greet('Greetings');
SayHi('Chris');
// returns "Greetings Chris"
```
This still returns the same result, which is probably as you expected as well. But, going back to the code line by line:

1. The greet('Greetings') created a ``greet() execution context``, and within this context, there is a variable `whattosay` with a *locally* stored value `'Greetings'`. 
2. When the *return* statement in the greet function get executed, the ``greet() execution context`` is now gone and removed. It returns the function 

```
function(name) {
       console.log(whattosay + ' ' + name);
   }
```

and store it into the SayHi variable.  Now the variable SayHi is actually exactly the function as above.

3. SayHi('Chris') now invokes the return function as above. It creates a ``SayHi() execution context``, which uses variable `whattosay` and `name` to create the console.log 
message. The question now is where is this `whattosay` value coming from, since the ``greet() execution context`` has been closed?

** The answer to goes back to the definition of a closure: a closure is a function having access to the parent scope, even after the parent function has closed **
Here, although the parent scope (i.e., greet() execution context) has been destroyed, the SayHi() function have access to its parent's variables which are remained. 

###[Example 2](http://www.w3schools.com/js/tryit.asp?filename=tryjs_function_counter3)

```
var add = (function () {
    var counter = 0;
    console.log('local: '+counter);
    console.log('this part will only be executed once in the initial immediately invoked function.')
    return function () {
        console.log('inner: '+counter);
        return counter += 1;
    }
})();

add();
add();
add();

// the counter is now 3
```

**Explanation:**

1. The part of function:

```
    var counter = 0;
    console.log('local: '+counter);
    console.log('this part will only be executed once in the initial immediately invoked function.')
```
will only be executed once in the first IIFE (immediately invoked function expression).

2. After the initial IIFE execution, the **return function** is now stored in the variable add.
You can think add as variable which only stored the return function expression:
```
    var add = function(){
        console.log('inner: '+counter);
        return counter += 1;
    }
```
3. whenever add is executed, it will look for the outside scope variables ```counter```. Although IIFE's execution context get closed, since it is the parent
scope of this return function, the add() will still get access to the variable `counter`. 
