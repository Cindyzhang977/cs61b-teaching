# Asymptotics
When we write code to solve a problem, we want to know how efficient our solution is. If we simply measured the time it takes for the program to execute, that measurement would vary depending on which machine we use, and even then the time would vary from trial to trial. Instead, we rely on asymptotic analysis to describe the efficiency of an algorithm based on the input size. **It's important to note that we only care about how the function would perform as inputs grow infinitely large.**

Let N be the input size, and let c be a constant. In order of fastest to slowest runtime: linear &Theta;(c), logarithmic &Theta;(logN), polynomial &Theta;(N<sup>c</sup>), exponential &Theta;(c<sup>N</sup>), &Theta;(N!), &Theta;(N<sup>N</sup>).

[Here](https://www.bigocheatsheet.com/) is a cheat sheet for the runtimes of different sorting algorithms and data structures.

## Notation
_Big-O_ (**O**) - upper bound

_Big-Omega_ (**&Omega;**) - lower bound

_Big-Theta_ (**&Theta;**) - tight bound (a &Theta;-bound exists when the tightest upper bound equals tightest lower bound)

**Note:** Big-O is not synonymous with "worst case" and Big-Omega is not synonymous with "best case". As an example, the worst cast runtime of a function could be &Theta;(N<sup>2</sup>), and it's perfectly acceptable to say that &Theta;(N!) is an upper bound for the function. Instead, we can say that the worst case is the _tightest_ Big-O bound, and the best case is the _tightest_ Big-Omega bound. 

## Quality vs. Quantity of Input
During runtime analysis, we only consider when the input is infinitely large. In other words, we always assume that the _quantity_ of the input is an infinitly large `N`. Therefore, we ignore the if-statement in `function1` since 1000 is a constant, and the runtime of `function1` is &Theta;(N). 
```
void function1(int x) {
  if (x < 1000) {
    return;
  }
  
  for (int i = 0; i < x; i++) {
    System.out.println(i);
  }
}
```

We do consider, however, the _quality_ of the input. To list some examples:
- If the input is an array, is the array is sorted? Is the first element the largest element in the array? (We always assume the length of the array is infinitely large.)
- If the input is a tree, is the tree balanced? (We always assume the number of nodes in the tree is infinitely large.)
- If the input is an integer, is that integer odd or even? Is it divisible by 3? (We always assume the integer is infinitely large.)

When analysing the runtime of `function2`, the if-statement considers the parity of `x`, which is a quality of the input, so we must break up the runtime between the best case and the worst case. The best case is if `x` is even, so the if-statement is satisfied and the function returns immediately, giving it a constant runtime &Theta;(1). The worst case is if `x` is odd, so the for-loop runs instead, giving it a linear runtime &Theta;(N). 
```
void function2(int x) {
  if (x % 2 == 0) {
    return;
  }
  
  for (int i = 0; i < x; i++) {
    System.out.println(i);
  }
}
```

## Calculating Runtime
First, let's walk through some definitions. When analysing the runtime of recursive functions, we often draw out a tree depicting the runtime at each recursive call. A **node** of the tree represents a single call to the function. The **work** done for a node is the runtime of that particular call of the function. The work done for a node is the value of that node. The **branching factor** of a node is the number of recursive calls it makes. The overall runtime or work of the entire function is the sum of all the work done at each node. 

Consider the following recusive method as an example:
```
int function3(int N) {
  if (N == 0) {
    return 0;
  }
  
  int total = 0;
  for (int i = 0; i < N; i++) {
    total += i;
  }
  
  return function3(N/2) + function3(N/2) + total;
}
```
Here is what the recursion tree looks like:
```
          N
      /       \
   N/2         N/2
  /   \       /   \
N/4   N/4   N/4   N/4
/ \   / \   / \   / \
         ...                               
```
The work done at the root node is `N`, since the for-loop iterates from 0 to N. The work done at the first level recursive calls are `N/2`, since the for-loop iterates from 0 to N/2. The branching factor of each node is 2, since two recursive calls are made. 

### Solving with Summations
This method, although sometimes tedious, would always work. For recursive methods, it involves finding the work done per node of the function and summing the work across all nodes to get the total work done. Similarly, for iterative methods, it involves finding the work done per iteration and summing the work across all iterations to get the overall runtime. 
```
void function4(int N) {
  for (int i = 0; i < N; i++) {
    for (int j = i; j < N; j *= 2) {
      System.out.println(i + j);
    }
  }
}
```
For the first iteration when `i = 0`, the inner loop iterates from 0 to N while multiplying by 2 each step, which incurs &Theta;(logN) work. When `i = 1`, the inner loop iterates from 1 to N, which incurs &Theta;(log(N - 1)) work. When `i = 2`, the inner loop iterates from 2 to N, which incurs &Theta;(log(N - 2)) work. Thus the overall summation is `log(N) + log(N - 1) + log(N - 2) + log(N - 3) + ... + log(2) + log(1)`. Applying log rules, this summation becomes `log(N * (N-1) * (N - 2) * ... * 2 * 1)`, which simplifies to `log(N!)`. 

#### Common Summations
1 + 2 + 3 + 4 + ... + (N - 1) + N = N(N+1)/2 = &Theta;(N<sup>2</sup>)

1 + 2 + 4 + 8 + ... + N/4 + N/2 + N = &Theta;(N)

1 + 2 + 4 + 16 + ... + 2<sup>N</sup> = &Theta;(2<sup>N</sup>)

### Solving with Multiplication 
This method is effectively unit conversion, and thus relies on either the work/node to be consistent across all nodes or the work/level to be consistent across all levels of the recursion tree. In equation form, `total work = (work / node)(# of nodes / level)(# of levels)` or simply `total work = (work / level)(# of levels)`. 

Let's revisit the recursion tree from `function3`, and calculate the runtime of the function. Is the work/node consistent across all nodes? No. Is the work/level consistent across all levels? Yes. Therefore, we can use multiplication to solve for the runtime of `function3`.
```
          N                    level 0 work: N
      /       \
   N/2         N/2             level 1 work: 2 * N/2 = N
  /   \       /   \
N/4   N/4   N/4   N/4          level 2 work: 4 * N/4 = N
/ \   / \   / \   / \
         ...                   leve k work: 2^k * N/(2^k) = N
```
Since there are logN levels (convince yourself why this is the case) and the work/level is N, the overall runtime is &Theta;(NlogN). 

Let's look at a more complicated example. 
```
int function5(int N) {
  if (N == 0) {
    return 0;
  }
  
  int total = 0;
  for (int i = 0; i < 10; i++) {
    total += function3(N - 1);
  }
  
  return total;
}
```
For clarity purposes, the branches of this recusive tree has been omitted.
```

```
