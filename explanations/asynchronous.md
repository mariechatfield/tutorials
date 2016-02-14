# What is asynchronous code execution?

Code is a series of instructions, which are run one at a time in sequential order. During normal code execution, an instruction in one function might call out to another function.

At this point, the instructions in the other function begin running and the original code is put aside for a moment.

When the other function is done, it returns to our original code with some return value. Our original code resumes its execution and can do something with that return value. We refer to this as **synchronous** execution.

![Synchronous Diagram](images/diagram_async_01.png)

However, some code operates outside the normal code execution. We refer to this as **asynchronous** execution, and it introduces the possibility for chaos into our otherwise orderly system. This is because the instructions of asynchronous code generally run at the same time as (and totally separate from) the instructions of the rest of our code. This code is doing things in its own happy world, and may (or may not) eventually return with a result.

For example, we might be running some Javascript on our website that needs some data from a server. We call a function that sends a request to the server to get that data.

This request is sent on our behalf, but it takes some time to get all the way there and back. In the meantime, the rest of our Javascript keeps running.

At some point, the request will complete and will return our data. But there's no way to get this data back to our original code.

![Asynchronous Diagram](images/diagram_async_02.png)

Instead of trying to get the data back to the original code to do something with it, we tell the asynchronous function what to do when it completes.

![Asynchronous Diagram with Callback](images/diagram_async_03.png)

In Javascript, this usually looks like passing a callback function as an argument.

```javascript
var do_something_cool = function (result) {
    console.log(result);
};

var original_function = function () {
    // You can define a function inline.
    other_function(function (result) {
        // this is called by function_that_does_something_asynchronous
        do_something_cool(result);
    });
};

var original_function = function () {
    // You can also pass a function by reference.
    // This will do the exact same thing as the example above.
    other_function(do_something_cool);
};

var original_function = function () {
    // But this would not work. Don't do this.
    var result = other_function();
    do_something_cool(result);
};
```

The documentation for an asynchronous function should tell you what types of data you can expect your callback function to receive, if you choose to provide a callback.