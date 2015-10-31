##Asynchronous Callbacks
Event: a single task occured in browser. For example, click handle event, HTTP request event (e.g., request data upload/download). 

####Event queue
The browser put events in event queue. For instance, mouse click, and HTTP request are two different events, and are placed in event queue in sequence. One event will not be executed until the event ahead in the queue is completed.


```javascript
// long running function
function waitThreeSeconds() {
    var ms = 3000 + new Date().getTime();
    while (new Date() < ms){}
    console.log('finished function');
}

function clickHandler() {
    console.log('click event!');   
}

// listen for the click event
document.addEventListener('click', clickHandler);

waitThreeSeconds();
console.log('finished execution');
```

If users click the mouse while waitThreeSecond is being executed (before the ``console.log('finished execution')`` being executed), the output from running the code is still:
```javascript
finished function
finished execution
click event!
```

Note that the clickHandler is not executed until everything in the event queue has been finalized including code in the global lexical enviroment (here, ``console.log('finished execution')`` is in the global enviroment)