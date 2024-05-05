# everything-frontend


# 1. What is hydration ?
A. Hydration is the process of using client-side JavaScript to add application state and interactivity to server-rendered HTML.

# 2. EventSource vs EventEmitter
A. - `EventSource`: Used in web development to receive real-time updates from a server.
- `EventEmitter`: Used in Node.js applications to facilitate communication between components through asynchronous event-based patterns

`EventSource`: In the context of web development, `EventSource` is a built-in JavaScript interface that allows the client to receive server-sent events. It establishes a persistent connection with the server and receives events or data updates over that connection. The server can send events at any time, and the client listens for those events using event listeners (`onmessage`, `onopen`, etc.). This is typically used for real-time updates from the server to the client.

- `EventEmitter`: In Node.js, an `EventEmitter` is a built-in class that facilitates communication between objects in an event-driven manner. It provides an implementation of the observer pattern, where objects can emit named events to which other objects (listeners) can subscribe. When an event is emitted, all subscribed listeners are notified and executed asynchronously. This pattern is commonly used for decoupled communication between different parts of a Node.js application.

# 3. Ways to Execute async functions in Series?
A. 1. using async/await 

const asyncSeriesExecuter = async function (promises) {
        for (let promise of promises) {
            try {
                const result = await promise;
                console.log(result);
            } catch (e) {
                console.log(e);
            }
        }
    }

2. Using recursion approach

const asyncSeriesExecuter = function (promises) {
        // get the top task
        let promise = promises.shift();
        //execute the task
        promise.then((data) => {
            //print the result
            console.log(data);
            //recursively call the same function
            if (promises.length > 0) {
                asyncSeriesExecuter(promises);
            }
        });
    }

3. Using reduce method

const asyncSeriesExecuter = function (promises) {
        promises.reduce((acc, curr) => {
            return acc.then(() => {
                return curr.then(val => { console.log(val) });
            });
        }, Promise.resolve());
    }
