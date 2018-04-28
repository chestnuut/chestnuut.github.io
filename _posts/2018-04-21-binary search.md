`this is just a algorithm learning blog for my own purpose of use.`
# Recursion I & Binary Search
## Recursion I
- function call itself;
- Boil down a big problem to smaller ones.
- **Implementation**:
    - *Base case*: smallest problem to solve;
    - *Recursive rule*. (Suppose we can solve the same problem with smaller size, what is left to do with current problem size).


### Fibonacci sequence

a classical problem on recursion.

### Time and space complexity analysis of recursion
1. draw recursion tree. in this example, Fib() can be described as n-level recursion tree. 
2. total **Time** is the number of nodes in this tree. so total is 2^n. total **Space** is the level of recursion tree (aka. call stack) is O(n).

### Optimal solution on fibonacci
1.  using dynamic programming. 
    - use an array store all result. this will lead to O(n) space and O(n) time.
    - use a variable to store result. when we receive the temp result, set b to temp and a to b. do it n times and we get the result in b.
2.  using matrix multiplication
    - This will lead to O(logn) time complexity and O(1) space
    - this method uses a fibonacci attributes in matrix.

    $$
        \begin{bmatrix}
            1&1 \\
            1&0 
        \end{bmatrix} *
        \begin{bmatrix}
            1&1 \\
            1&0 
        \end{bmatrix} = 
        \begin{bmatrix}
            2&1 \\
            1&1 
        \end{bmatrix}
    $$
    $$
        \begin{bmatrix}
            2&1 \\
            1&1 
        \end{bmatrix} *
        \begin{bmatrix}
            1&1 \\
            1&0 
        \end{bmatrix} = 
        \begin{bmatrix}
            3&2 \\
            2&1 
        \end{bmatrix}
    $$
    $$
        \begin{bmatrix}
            3&2 \\
            2&1 
        \end{bmatrix} *
        \begin{bmatrix}
            1&1 \\
            1&0 
        \end{bmatrix} = 
        \begin{bmatrix}
            5&3 \\
            3&2 
        \end{bmatrix}
    $$
    $$\dots$$

    - we can infer that matrix[0][0] is the fib(n) we want to calculate. then we can use a^b trick to decrease the running time to O(logn).

### Calculate **$a^b$**

Time $O(logN)$ Space $O(logN)$
- think about we already know the result of $a^{b/2}$, then we just need to multiply $a^{b/2}*a^{b/2}$. If b is odd, just multiply another a.

## Binary Search
The principle of binary search is to **reduce the search space by half** of its original size. In the meantime, you must guarantee that the target must **not be ruled out**. 

### Classical Binary Search
if need only one result, left<= right.
if need multiple result, need to control the distance between left and right.
after calculate mid point, remember to set right = mid-1,left = mid+1 to ensure the search size is smaller than before.

### search in 2D space
- Method 1: binary search find row first, then find col.
- Method 2: consider the matrix as a whole. we can get the index of the matrix by 
    > row = ${mid}/cols
        
    > col = ${mid}%cols

    Then we can simply do binary search in 1D.

Time O(log(M*N))  

### First & Last Occurrence && Closest in sorted 1D array

The key point is to maintain two elements after binary search. The trick is to use `while(left < right - 1)`. We have left point to an element and right point to another, do a post-processing would lead to final result.

### Kth Closest in sorted 1D array
- Method 1: $O(logn+k)$ 
    - step1: binary search find the largest smaller or equal element's index. marked as left; right = left + 1.
    - step2: 谁小移谁。if left is smaller then move left pointer --.
    - worked if we want to return a whole list of elements since we can't get rid of k.
- Method 2: $O(logn + logk)$
    - If we only need the kth value we can use not only binary search to find target, but also use augment binary search to find kth value closest to target.

### find max in a half increment, half decrement array.
we can use binary search on some partially sorted array, like this. 1,2,3...100, 99, 98, ... find the max in this array.
The only difficulty is to analyze the different situation when should we return "mid".

### Search in unknown size sorted array
The key is to using find mid in linkedList technique, jump to the target value's closest left and right indices. Will save a lot of time. Total Time is log(n)+log(2n) -> O(log(n))


