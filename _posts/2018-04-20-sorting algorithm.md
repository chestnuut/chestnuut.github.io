`this is just a algorithm learning blog for my own purpose of use.`
# Sorting Algorithm
## selection sort
1. find global min 
2. put it on the left-most index in current range.
3. find global min in the remain element.
4. repeat

**Time Complexity**

first loop: n

second loop: n - 1

...

time=O(n + (n-1)+(n-2)+...+1)=(n+1)*n/2=O(n^2)

### Related topic
- Sort a stack using two stacks
    
    1. pop the original stack, if e < stack1.peek() push.
    2. else push stack1.pop() in stack2. 
    - since we maintain a decreasing order in stack1. then stack1.peek() is always the smallest value in the given array.
    - Time: O(n^2) size of original stack
    - Space: O(2n) additional two stacks

- Sort using only one stack

    1. use a global_min variable to store current min value;
    2. If encounter a value bigger than peek of tmp_stack, pop this value push back to the original stack. 
    3. repeat 2 until e < tmp_stack.peek()
    - Time: O(n^2)
    - Space: O(n) 

## Merge Sort

devide to small part then merge together.

Time Complexity: O(nlogn) Space: O(n)

Merge Sort is useful in external sort.

### Related Topic
- Merge Sort a LinkedList
    1. same procedure. Instead of O(n) space, LinkedList only needs O(1) space.
    2. find middle point. Remeber to handle the left half head node and the right half head node.
- A1B2C3D4 to ABCD1234
    1. The only difference is in merge function. Instead of "谁小移谁"，using ASCII to distinguish which char is a letter or number. [0~9]->[48~57] [A]->65
- ABCD1234 to A1B2C3D4
    1. we can use recursion. think about how to get AB12CD34("I like yahoo -> yahoo like I" trick), then use recursion on left side and right side.
    2. For string exactly 2^n length, we can use bitwise rotate to achieve O(n) time, O(1) space. Since every char index except 0 and n-1 is swapped following a rule. In this case, (1,4,2) and (3,5,6). They can be considered as 001 -> 100 -> 010 && 011 -> 101 -> 110. right shift 1 bit with rotate. 
    3. rotate can be achieved by 
    ```java
        (i>>>1 | i << (logn - 1)) & (size - 1)
    ``` 

## Quick Sort

Select pivot randomly. swap to the final position. make sure the left side of pivot is smaller than pivot, the right side of the pivot is larger than pivot. swap back.
Do recursion on left and right side.

Worst Time: O(n^2) , average O(nlogn) normally quicker than mergesort.

### Related Topic 
挡板题
- Array Shuffling: move all 0s to the end of array.
- Character removal from a string
- Quick partition problem
- Rainbow sort (3个挡板，4个区域)

