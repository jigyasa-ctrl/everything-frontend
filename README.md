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


# explain browser caching using service workers and benefits over http caching

# HTTP caching
HTTP caching is a technique used by web browsers to store previously accessed web resources locally on the user's device. When a user revisits a page, instead of re-requesting all resources from the server, the browser can check its cache to see if it already has a copy of the resource. If it does, it can use the cached version, which speeds up page loading and reduces server load.
it relies on headers sent by the server (such as Cache-Control and Expires) to specify how long the browser should cache a resource and under what conditions it should be considered stale.

# Service Workers
Service workers are scripts that run in the background of a web application, separate from the web page. They can intercept and handle network requests made by the web page, allowing developers to control how resources are fetched, cached, and served to the user. Service workers enable features like offline access, push notifications, and advanced caching strategies.

# Benefits of Service Workers for Caching:

Offline Support: Service workers enable offline access to web applications by allowing developers to cache essential resources and serve them even when the user is offline. This is not possible with traditional HTTP caching alone.

Performance: Service workers can cache resources proactively, even before they are requested by the user. This prefetching capability can significantly improve page load times

Customizable Caching Strategies: Service workers can implement advanced caching strategies such as stale-while-revalidate, cache-first, network-first, or a combination thereof. This flexibility allows developers to optimize resource delivery based on factors like network conditions, resource importance, or user preferences.

Reduced Server Load: By serving cached resources directly from the user's device, service workers can reduce the number of requests sent to the server

Improved User Experience: Faster page load times, offline access, and seamless transitions between online and offline modes contribute to an improved overall user experience, leading to higher user engagement and satisfaction.

# different caching strategies for service workers

Cache-First: In this strategy, the service worker checks the cache first for the requested resource. If the resource is found in the cache, it's served directly to the user. If the resource is not in the cache, the service worker fetches it from the network, stores a copy in the cache for future use, and then serves it to the user.

Network-First: This strategy prioritizes fetching resources from the network. The service worker first attempts to fetch the resource from the network. If the network request fails (e.g., due to poor connectivity), the service worker serves the resource from the cache if it's available. If the resource is not in the cache, a fallback response (e.g., a custom offline page) can be served to the user.

Cache-Only: In this strategy, the service worker serves the resource only if it's available in the cache. If the resource is not cached, the service worker responds with an error or a fallback response. This strategy is useful for ensuring that critical resources are available offline but may result in incomplete page loads if essential resources are missing from the cache.

Network-Only: This strategy fetches the resource exclusively from the network without consulting the cache. It's useful for resources that should always be up-to-date and cannot be served from the cache. However, it doesn't provide offline support for these resources.

Cache-Falling-Back-to-Network: Also known as "Stale-While-Revalidate," this strategy serves the cached version of the resource to the user while simultaneously fetching a fresh copy from the network in the background. If the network request succeeds, the cache is updated with the new version of the resource. This strategy ensures fast page loads while keeping the cache up-to-date.

Cache-Then-Network: This strategy involves serving the cached version of the resource to the user immediately while also fetching a fresh copy from the network in parallel. The user is served the cached version first, and if the network response differs (e.g., due to an update), the cache is updated accordingly for future requests.

# service worker vs web worker

Service workers are scripts that run in the background of a web application, separate from the main browser thread. They are designed to handle tasks like network requests, caching resources, and enabling features such as offline access and push notifications

Web workers are also scripts that run in the background of a web application, but their primary purpose is to offload CPU-intensive tasks from the main browser thread. They are used for tasks such as complex calculations, data processing, or continuous background tasks.

# What is the difference between debouncing and throttling?

● Debouncing :- It is used to invoke/call/execute functions only
when things have stopped happening for a given specific time.
For example, Call a search function to fetch the result when the
user has stopped typing in the search box. If the user keeps on
typing then reset the function.

● Throttling :- It is used to restrict the no of time a function can be
called/invoked/executes. For example, making an API call to the
server on the user’s click. If the user spam’s the click then also
there will be specific calls only. Like, make each call after 10
seconds.

