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
```
function foo(...args) {
  console.log(args[3]);
}

var arr = [ 1, 2, 3, 4, 5 ];

foo(...arr); // 4
```
In a value-list position, it spreads. In an assignment position -- like a parameter list, because the arguments get assigned to the parameters -- it gathers. Use it instead of slice(), concat(), and apply() when working with arrays.

- Destructuring: {} or [] on left of "=", or inside parameter list.
Extract data from objects, arrays, maps, and sets into their own variable.
```
function foo([x, y, ...args]) {
 ...
}

foo([1, 2, 3]); // x: 1, y: 2, args: [3]

const { first, last } = person;
```

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

Types:
1. Vertical: faster CPU, more RAM, more disk space
2. Horizontal: more CPUs, more servers
- more difficult since it adds complexity to the system. It requires system to handle parallel processing, and to account for data being physically distributed.
- Prevalent solution for distributed data is NoSQL. They are highly scalable, although it has some drawbacks. See [Redis](https://github.com/joriguzman/programming-notes/#redis).

How to scale an app:
[TODO]
