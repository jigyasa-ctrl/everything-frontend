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

# Slice vs Splice ?

Use slice() to create a new array containing a subset of elements from the original array without modifying the original array.

eg -> const fruits = ['apple', 'banana', 'orange', 'grape', 'kiwi'];
const citrus = fruits.slice(2, 4);
console.log(citrus); // Output: ['orange', 'grape']


Use splice() to modify the original array by removing, replacing, or adding elements in place.

eg -> 
syntax - array.splice(start, deleteCount, item1, item2, ...)

const numbers = [1, 2, 3, 4, 5];
numbers.splice(2, 1); // Removes one element starting at index 2
console.log(numbers); // Output: [1, 2, 4, 5]

numbers.splice(2, 0, 6, 7); // Inserts elements 6 and 7 at index 2
console.log(numbers); // Output: [1, 2, 6, 7, 4, 5]

# What techniques do you use to ensure responsive design in your projects?

I follow a mobile-first approach, using CSS grid and flexbox for fluid layouts, relative units instead of fixed pixels(%, em, rem, vw/vh etc), and media queries for breakpoints. I rely on modern techniques like clamp() for responsive typography and srcset/picture for responsive images. I also test designs in Chrome DevTools and real devices to ensure a consistent experience. For React apps, I sometimes pair this with utility-first CSS like Tailwind to manage responsiveness efficiently.

# Can you describe a challenging project and how you overcame obstacles?

In one of my recent projects, I was building a frontend application that integrated AI-powered code review using a local LLM (Ollama) with a Next.js UI. The challenge was that the LLM responses were slow and unpredictable, and on the frontend, this caused UI freezes and poor user experience.This turned the app from a laggy experience into a smooth, interactive one. 

# how to maintain smooth animation while maintaining 60fps on low end device??

To maintain 60fps even on low-end devices, I ensure animations run on the GPU-friendly properties like transform and opacity instead of layout-triggering ones like transition top, width, etc. I optimize event-driven animations with requestAnimationFrame, and use CSS transitions when possible since they bypass the JS thread. For heavy lists, I use virtualization, and for computationally expensive work, I offload to Web Workers or break into smaller chunks. I also profile with DevTools to detect dropped frames and optimize accordingly.

transform (translate, scale, rotate)

window.addEventListener("scroll", () => {
  requestAnimationFrame(onScroll);  // ✅ smooth sync with paint cycle
});

# how to prevvent memory leaks in long running application react??
In React, memory leaks usually happen when we leave behind subscriptions, async requests, or event listeners after a component unmounts. I prevent them by always cleaning up effects with return in useEffect, canceling fetch requests with AbortController, clearing timers, and removing event listeners. For long-running apps, I also monitor memory usage in DevTools to ensure no detached DOM nodes or unused listeners pile up.

# What is the type of null? Why is it an object?
typeof null returns "object" because of a historical bug in JavaScript’s implementation.
This was a bug, but it got locked into the language for backward compatibility.
In reality, null is a primitive type, not an object.

# Controlled Components vs uncontrolled Components ?
Controlled components are the components which are controlled by the reacr states. Use these when comp needs to update state on render.
use these for dynamic behaviour like showing the password strength as and when the user types.

uncontrolled comp are controlled by DOM. Use this one when the details are only required at the end. eg in forms. Use semantic HTML + useRef to get data from forms.
use them if u just have a basic html form and extract values from form at the end of the submisssion.

Example -> form, counter

# transform vs translate in CSS ?
transform is a CSS property that applies 2D or 3D transformations to an element (translate, rotate, scale, skew, etc.).

translate(...) is one of the transform functions — it moves (shifts) an element along X / Y / Z axes without affecting document flow.

Translate - Does not affect layout flow — translated elements still occupy their original position for layout (no reflow).
transform is GPU-friendly, so animating transform (and opacity) is preferred for smooth animations.

# What is event delegation ?

Event delegation is a pattern where you attach a single event listener to a parent element to handle events from its child elements, instead of attaching separate listeners to each child.
It works because of event bubbling: when an event is fired on a child, it bubbles up through its ancestors, so the parent can "catch" it.
Performance → fewer event listeners = less memory usage.
Dynamic elements → works even for elements added later to the DOM.
Cleaner code → one handler for many elements.

# useEffect vs uselayoutEffect() ?
useEffect → async, runs after paint → does not block UI.
useLayoutEffect → sync, runs before paint → can block UI if heavy.

Rule of thumb:
Use useEffect for most side effects. for API calls, subscriptions, logging, timers.
Use useLayoutEffect only when you need to measure or synchronously modify the DOM before paint. for measuring DOM, scroll sync, animations.

# What is code splitting and how do you do it in React

Code splitting is splitting large JS bundles into smaller chunks that load on demand. In React, we usually do it with React.lazy and Suspense, or at the routing level, so the app loads faster and only downloads code when required.
