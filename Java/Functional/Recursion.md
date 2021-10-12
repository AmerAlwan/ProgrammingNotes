# Recursion

  ## Types of Recursion

### Single & Multiple Recursion

#### Single

Recursion that contains a single self-reference. Single recursion is often more efficient and can be replaced with a literation like a `for` or `while` loop. 

A single recursion would usually run in linear time and require constant spacer

Examples include:

- List Traversal
- Linear Search
- Computing factorial function

#### Multiple

Recursion that contains multiple self-references.

Examples Include:

- Tree traversal
- Depth-first Search

### Structural Recursion

Recursion where the parameter passed is part of the original data

### Generative Recursion

Recursion where the parameter passed in does some operation on the original data (Ex: Greatest Common Divisor function à gcd(n2, n1 % n2)