# Big-O Notation
Tells you how complex an algorithm is. It describes the execution time or space used by an algorithm. It generally implies the worst case scenario, unless explicitly described as best case. For example, we could say this is worst case O(n) and best case O(1).

It can be expressed in terms of either runtime or space (additional memory cost).

Think about the time and complexity of algorithms as you design them, but be aware of premature optimization. Find the right balance between runtime, space, coding time, readability, and maintainability.

"O" stands for "Order" e.g. O(1) is "Order 1".

- O(1) - constant complexity. Example: accessing an array by index

  1 item: 1 operation, 100 items: 1 operation

- O(log n) - logarithmic complexity. Example: binary search tree

  1 item: 1 operation, 100 items: 3 operations, 10000 items: 5 operations

- O(n) - linear complexity. Example: counting number of items in a list, reading a book

  1 item: 1 operation, 10 items: 10 operations, 100 items: 100 operations

- O(n log n) - time to complete increases by the number of items times Log2(n). Example: quick sort, heap sort

- O(n^2) - quadratic. Examples: loop within a loop, bubble sort

- O(2^n) - exponential, increases based on the exponent N of constant 2 (or C). Example: travelling salesman solved using dynamic programming 

- O(n!) - factorial of the input set. Example: travelling salesman brute-force solution

- O(infinity) - tossing a coin until it lands heads/tails

As a rule of thumb, anything with N^2 or any other exponent is not a good algorithm.

### Links
1. [Interview Cake](https://www.interviewcake.com/article/javascript/big-o-notation-time-and-space-complexity) - clear and concise explanation
2. [Big O cheat sheet](http://bigocheatsheet.com/)

# Functional Programming
Functional programming is about writing pure functions and minimizing impure functions.
A **pure function**:
- Given the same input, will always return the same output
- Produces no side effects e.g. writing to database, console.log()
- Does not rely on external mutable state

A pure function is has referential transparency, meaning it can be replaced with its corresponding value without affecting program behavior. Half(4) can be replaced with 2 wherever in the code without affecting the final outcome.

Benefits:
- Dramatically reduced multithreaded and concurrent code, because you don't need to worry about one thread mutating the value of shared state between multiple threads. You don't have to worry about deadlocks and race conditions because you don't need to use locks.
- More terse and expressive code
- Less boilerplate code compared to object-oriented languages which are heavily dependent on design patterns
- Easier to test
- Easier to debug

In functional programming:
- Core functionality is implemented using pure functions, and impure functions are minimized
- Data is immutable
- Functional programs are stateless
- Imperative code container manages side effects and executes declarative, pure code

### Links
1. [Modern Javascript concepts](https://auth0.com/blog/glossary-of-modern-javascript-concepts/)
2. [What is a pure function?](https://medium.com/javascript-scene/master-the-javascript-interview-what-is-a-pure-function-d1c076bec976)

# Tips
- Look for a [greedy](https://en.wikipedia.org/wiki/Greedy_algorithm) approach when solving a problem. A greedy algorithm iterates through the problem space, taking the best answer so far, until it reaches the end. Greedy approaches usually lead to O(n) time.
- Look up hash table (see what I did there?) most of the time helps to optimize the solution.

# JavaScript
- Rest / Spread operator: "..."
In a parameter list, it "gathers" the arguments together and puts them in an array. In an argument list, it spreads them out into individual arguments.

Spread: value context; right handle of equals; as argument
```
const arr = [ 1, 2, 3, 4, 5 ]

const newArr = [...arr] // Copy of arr
```

Rest/Gather: assignment context; left hand of equals; as parameters, because the arguments get assigned to the parameters
```
function foo(a, b, ...args) {
  console.log(args[1])
}

foo(1, 2, 3, 4) // outputs 4
```

Use it instead of slice(), concat(), and apply() when working with arrays.

- Destructuring: {} or [] on left of "=", or inside parameter list.
Extract data from objects, arrays, maps, and sets into their own variable.
```
function foo([x, y, ...args]) {
 ...
}

foo([1, 2, 3]); // x: 1, y: 2, args: [3]

const { first, last } = person;
```

- `this` depends on how the function is called. See object on left of the dot (.) for its context.
1. `person.sayHi()` - `this` refers to person
2. `sayHi()` - `this` is global Window object, or undefined in strict mode
3. `call` / `apply` / `bind` - `this` is set to the first argument e.g. `summary.call(book)`
4. In arrow functions, `this` is taken from enclosing execution context i.e. outer function:
```
function myFunc() {
  this.myVar = 0;
  setTimeout(
    () => { // this taken from surrounding, meaning myFunc here
      this.myVar++;
      console.log(this.myVar) // 1
    },
    0
  );
}
```
5. In setTimeout(), Javascript engine calls the method and `this` refers to the Timeout object! Use bind() to preserve this:
`setTimeout(kurt.greet.bind(kurt), 1000)`

https://www.taniarascia.com/this-bind-call-apply-javascript

https://javascript.info/object-methods#arrow-functions-have-no-this


# Tips
- Always name functions instead of writing anonymous functions, for stack trace debugging, readability, and reliable self-reliance.
```
setTimeout(function waitForIt() {
  if (!o.it) {
    setTimeout(waitForIt, 100);
  }
}, 100);
```
Be careful when using using arrow functions. They are convenient to write, but as the cost of readability.

- Don't use "this"-aware functions due to confusions in "this". You should not be using "this" in Functional Programming because "this" is an implicit input for your function. In FP, prefer explicit inputs and outputs. 

# Database
ACID - properties of database transactions
- Atomicity - all parts of a transaction is committed, or none at all.
- Consistency - transaction never leaves the database in a half-finished or invalid state.
- Isolation - transactions are separate from each other until they are finished.
- Durability - once transaction is completed, changes are permanent. In case of failure, changes should not be lost.

## Redis
- A key-value data store where the entire data set is stored in-memory so it is extremely fast.
- It has built-in persistence, the data won't disappear when system is restarted.
- It is a good choice if you want a highly scalable data store shared by multiple processes, apps, or servers.

Use cases:
1. Show latest item listings in your home page
2. Deletion and filtering cached items
3. Order by user votes and time, just like Reddit
4. Leaderboards and related problems, where results change frequently over time

Drawbacks:
1. In-memory, so data size is limited by memory size.
2. No query language (only commands). You cannot submit ad-hoc queries. All data access must be anticipated by the developer. A lot of flexibility is lost.
3. It is not a relational database. Foreign key means nothing. Referential integrity is not maintained by Redis, and must be enforced by the client app.
4. No D in ACID, meaning an executed command is not guaranteed to persist to disk since Redis only flushes to disk at configurable intervals. It should not be used as primary storage for data you cannot afford to lose. But Redis supports different persistence options, from "not safe but very efficient", to "safe but not very efficient". It also supports master-slave replication to protect the data in case of complete node failure.

### Links
[What is Redis for](https://stackoverflow.com/questions/7888880/what-is-redis-and-what-do-i-use-it-for)

# Scalabilty
It is the ability of a system to handle growing amounts of work in a graceful manner, or the potential to handle that growth. It is not about speed or performance.

Before scaling, gather data and profile your system. Find out what resource needs scaling: Memory, CPU, Network I/O, or Disk I/O. Measure things like:
- Concurrent gequests per second
- Average response time per request
- Number of records processed per second/minute

Don't prematurely optimize, nor spend time over-optimizing, because it introduces complexity, abstraction, and apps that are harder to maintain and test.

Types:
1. Vertical: adding more power to existing machine e.g. faster CPU, more RAM, more disk space
- System is turned off while upgrading
- Can only be done a certain number of times before capacity is maxed out
2. Horizontal: more CPUs, more servers
- More flexible, you don't need to take server offline while scaling
- More difficult since it adds complexity to the system. It requires system to handle parallel processing, and to account for data being physically distributed.

Prefer horizontal to vertical scaling, since it is cheaper and more flexible

How to make app scalable:
- Caching: store results of common operations, reuse data even if it's a bit stale
- Use a load balancer, so you can horizontally scale by adding new servers. Since it's a one-time setup, you should consider doing it up-front.
- Scale up database using indices, query optimization
- Avoid doing complex operations in the request-response cycle. Run them "offline" using a separate pool of workers.
- Use caching with Memcached / [Redis](https://github.com/joriguzman/programming-notes/#redis), or a distributed data store such as Hazelcast
- Separate web server with database server
- Create stateless web architecture: session state is not be stored in any one particular server and responses and not dependent upon data from a previous session. Use REST API. If you must save state, save it on the client.
- Use service-oriented / microservices arhictecture, such that the app is a suite of small services, and each service is self-contained and independent. The app has its own independent web, application, caching, and database tiers. This way, you can scale a component or service on its own without affecting other components.

Client-side improvements:
- Minimize HTTP requests. 80-90% of end-user response time is spent downloading a page's components: images, stysheets, scripts, etc.
  - Combine files using a module bundler like Webpack
  - Use CSS Sprites, combining images into a single image and using CSS to display the desired image
- Use a Content Delivery Network (CDN), a collection of web servers distributed across multiple locations to deliver content more efficiently
- Put stylesheets at the top
- Put scripts at the bottom
- Minify Javascript and CSS

### Links
[JavaScript Cheatsheet](https://mbeaudru.github.io/modern-js-cheatsheet)
[Scaling Your Web App](https://blog.hartleybrody.com/scale-load)
[Yahoo's Best Practices for Speeding Up Website](https://developer.yahoo.com/performance/rules.html)
[Stateless web architecture](https://www.quora.com/What-is-stateless-and-statefull-web-architecture)
