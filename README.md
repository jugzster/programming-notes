# Programming Notes

## Big-O Notation
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

- O(n!) - factorial of the input set. Example: travelling salesman brute-force solution

- O(n^2) - loop within a loop

- O(infinity) - tossing a coin until it lands

As a rule of thumb, anything with N^2 or any other exponent is not a good algorithm.

### Links:
1. [Interview Cake](https://www.interviewcake.com/article/javascript/big-o-notation-time-and-space-complexity) - clear and concise explanation
2. [Big O cheat sheet](http://bigocheatsheet.com/)
