## 2024 UWB CSS 342(A) Final Exam (60pt)

**Date: 8/15/2024**

**Time: 11:15 am to 1:15 pm PDT**

**Submission: Put your answers in a document like Word, PDF, or plain text, and submit it on Canvas**

**Late policy:** Any submission after 1:15 pm is considered late, and will NOT be accepted. Tip: add an alarm clock for 1:10 pm to remind yourself.

**Rules:**

- Open "book". Internet search also OK. Give reference to what you used from internet.
- Not required to come to school or zoom.
- Be very careful of potential bogus answer from ChatGPT. It's really meant to be used for learning, not for getting answers. 
- No communication (talk, text messaging, discord private and public messaging) of any kind with other students taking this exam during the exam.
- Ask question to instructor on discord in a **private** message. Public message will be ignored. 

Any violation will strip you of all the points and will be reported to school for disciplinary action. No exception.

**Tips:**

- Control your time spent on each problem. If stuck, move along and come back again later. Finish the easier ones first.
- Keep an eye on the Discord #midterm channel for updates.
- It might help if IDE like Intellij is used to write code.
- Read questions carefully. Is it asking for ***correct*** or ***incorrect***.
- Extra credits are pretty much free points to help your exam grade, so take it.


**1. (2pt) Explain why insertion sort has time complexity of O(n^2)? Use the number of comparsion for the explanation. Show the number of comparison adds up to O(n^2).**
```
Outer loop run from index 1 to k-1. Run a total of k-1 times 

For each element in the outer loop, the algorithm compares it with the elements in the sorted portion of the array (elements to its left) to find the correct position. For the 𝑖 i-th element, there could be up to i−1 comparisons.

The total of comparison can be seen as sum of k - 1 integer so sum is ((k-1) * k ) / 2 = (k^2 - k) / 2. Simplify to just O(n^2)  time complexity
``` 

**2. (4pt) Given the following coode, answer the questions.** 

```java
void bubble_sort(std::vector<int> &data) {
    size_t length = data.size();
    if (length < 2) {
        return;
    }

    for (int i = 0; i < length; i++) {
        for (int j = 0; j < length-1; j++) {
            if (data[j] > data[j + 1]) {
                swap(data, j, j + 1);
            }
        }
    }
}

void swap(std::vector<int> &data, int i, int j) {
    int tmp = data[i];
    data[i] = data[j];
    data[j] = tmp;
}
```

2.1 (2pt) The loops are doing redundant work making more comparisons than necessary. Describe what the redundant work is, and how to reduce the number of comparison in the loops by changing code in just one line. Show the line of code with your fix.
```
for (int j = 0; j < length - 1 - i; j++) 

Fixed : 

for (int j = 0; j < length - 1 - i; j++) // no need to compare the last one as it is already sorted 
```

2.2 (2pt) After reducing the number of comparison, is the complexity still O(n^2)? Explain your reasoning.
```
Yes, because outer loop still run n times and inner loop runs approximately n−i times, where  i ranges from 0 to 𝑛 − 1. 

The dominant term is still n^2. It did not get rid of the quadratic growth for n
```

**3. (2pt) Prove "x > 15 && y<30" and "!(x <= 15 || y>=30)" are logically equivalent. Must use and show the truth table.**
```
P = x > 15
Q = y < 30 
P
Q
P && Q 
T
T
T
T
F
F
F
F
F
F
T
F



!P
!Q
!( !P || !Q )
F
F
T
F
T
F
T
T
F
T
F
F



```

**Extra credit (2pt) Prove the following two function are logically equivalant using truth table.**

Logic equivalence can be used to simplify coding. Here's an example of removing the unnecessary "else {}" by flipping the logic in the if statement.

```
void function1(int x, int y) {
    if (x > 15 && y < 30) {
        printf("the result of the function\n");
    } else {
        printf("invalid input\n");
    }
}

void function2(int x, int y) {
    if (x <= 15 || y >= 30) {
        printf("invalid input\n");
        return;
    }
    printf("the result of the function\n");
}
```
Use truth table to prove that function1 and function2 are equivalent in logic.

```
P = x > 15
Q = y < 30 
P
Q
P && Q 
T
T
T
T
F
F
F
F
F
F
T
F



!P
!Q
( !P || !Q )
F
F
F
F
T
F
T
T
F
T
F
F





```


**4. (2pt) Fix the issue in the following code.**

Hint: you can use this [online c++ editor](https://www.onlinegdb.com/online_c++_compiler) to play with the code.

```c++
int& square(int num) {
  int result = num * num;
  return result;
}
int main()
{
    const int size = 10;
    int *data = new int[size];
    for (int i=0; i<size; i++) {
        data[i] = square(i);
    }
    for (int i=0; i<size; i++) {
        cout<< "value is " << data[i] << endl;
    }
}
```

Describe what the issue is, and show your fix with code.
```

int result = num * num; // 'result' is a local variable
 return result; // Returning a reference to a local variable

Fixed: 

int square(int num) { // Return by value
 return num * num;
 }


```

**5. (5pt) Given the following code:**

```c++
#include <iostream>
class BaseClass {
protected:
    int capacity;
    int *data;
public:
    BaseClass() = default;
    BaseClass(int capacity) {
        if (capacity < 1) {
            return;
        }
        data = new int[capacity];
        for (int i = 0; i < capacity; i++) {
            data[i] = i + 2;
            std::cout << "I hate C++" << std::endl;
        }
    }
    virtual int get_capacity() = 0;
    int operator[](int idx) {
        return data[idx];
    }
    ~BaseClass() {}
};
class DerivedClass : public BaseClass {
public:
    DerivedClass(int capacity) {
        this->capacity = capacity;
        data = new int[capacity];
        for (int i = 0; i < capacity; i++) {
            data[i] = (i % 3 == 0) ? (i + 30) : (i + 10);
        }
    }

    int get_capacity() {
        return capacity;
    }
    ~DerivedClass() {
        delete[]data;
    }
};

int main() {
    BaseClass *p_base = new DerivedClass(10);
    for (int i = 0; i < p_base->get_capacity(); i++) {
        std::cout << (*p_base)[i] << std::endl;
    }
    delete p_base;
}
```


**5.1 (2pt) In the following line, what does "=0" mean?**
```
    virtual int get_capacity() = 0;
```

```
// Taken from chatgpt 
The = 0 syntax is used to declare a function as "pure virtual." A pure virtual function does not provide an implementation in the base class and must be overridden by derived classes.


```

**5.2 (3pt) Running the code with Valgrind shows memory leak. How to fix it without changing any member function body (the part between { and })?**
```
==22708== LEAK SUMMARY:
==22708==    definitely lost: 40 bytes in 1 blocks
```

```
virtual ~BaseClass() { // Make the destructor virtual 
delete[] data; // Ensure data is properly deleted
 }

    ~DerivedClass() { // no need to do anything since you don’t want to double deleting stuffs 
    }

```

**Answer the following questions about tree ADT.**

**6.1 (15pt) What's the pre-order, in-order and post-order traversal of the following binary tree**
```bash
         5
        / \
       4   7
      /     \
     1       9
            /
           6
```

```

(5pt) pre-order: 5, 4, 1, 7, 9, 6


(5pt) in-order: 1, 4, 5, 7, 6, 9


(5pt) post-order: 1, 4, 6, 9, 7, 5
```

**6.2 (2pt) Is this tree a BST (binary search tree)? If not, change the value of exactly one node and make it a binary search tree.**
```
         5
        / \
       4   7
      /     \
     1       9
            /
           8




```

**6.3 (3pt) Given the root node of a binary tree, write the code that deletes the tree. This means delete all the nodes in the tree without memory leak.**
```c++
template<class T>
class BinaryTree;

template<class T>
class TreeNode {
public:
    friend class BinaryTree<T>;

    T val;
    TreeNode<T> *left;
    TreeNode<T> *right;

public:
    TreeNode() : left(nullptr), right(nullptr) {}

    TreeNode(const T val) : TreeNode() {
        this->val = val;
    }
};

template<typename T>
void delete_tree(TreeNode<T> *tree) {
    if (tree == nullptr) {
        return;
    }

    delete_tree(tree->left);
    delete_tree(tree->right);

    // Delete the current node
    delete tree;
}


```

**7. (5pt) Answer questions about Fibonacci sequence.**
Fibonacci sequence is a sequence of numbers where each number is the sum of the two preceding ones, starting from 0 and 1.
```
F(0) = 0, F(1) = 1
F(n) = F(n - 1) + F(n - 2), for n > 1.
```

Here are some examples:
```
Input: n = 2
Output: 1
Explanation: F(2) = F(1) + F(0) = 1 + 0 = 1.

Input: n = 4
Output: 3
Explanation: F(4) = F(3) + F(2) = 2 + 1 = 3.
```

**7.1 (2pt) Write code and generate the nth number in a Fibonacci sequence. Your code should run as efficiently (fast) as possible. Read 7.2 before writing the code here.**
```c++
#include <iostream>
using namespace std;
int fib(int n) {

    if (n <= 1) { return n ;} 

    int prev1 = 0, prev2 = 1;
    int result = 0;

    for (int i = 2; i <= n; i++) {
        result = prev1 + prev2;
        prev1 = prev2;
        prev2 = result;
    }

    return result;
}

int main()
{
    cout << fib(10);
}

Print : 55 

```


**7.2 (3pt) Explain what is "repeated sub-problem" in recursion? and explain that your code above for fib(int n) does NOT have this problem.**
```
// Got help from chatgpt
In a recursive implementation of the Fibonacci sequence, the function calls itself multiple times for the same input values.

The code provided above does not have the problem of repeated sub-problems because it is implemented iteratively, not recursively:
In the iterative approach, each Fibonacci number is calculated once and stored in a variable (either prev1, prev2, or result).


```

**8. (2pt) Explain how LRU (as defined [here](https://github.com/a-teaching-goose/2024-summer-342-hw-3/blob/main/src/problem_1/LRU.hpp)) can make search faster.**
```
In the code, Hashmap stores pointers to nodes which allows you to quickly find data in O(1) time. 

The linked list keeps track of the order in which elements are used. The most recently used item is at the front, and the least recently used item is at the back allowing the next search to be faster. 

```

**9. (3pt) In [this matrix multiply](https://github.com/a-teaching-goose/2024-summer-342-demo-caching-bigO-matrix-multiple/blob/main/main.cpp#L36), a whoppping 6-loop is used and yet this code runs much faster than the naive 3-loop matrix multiply. Explain why this code is faster than the "naive" 3-loop version.**

Here's an example of the running time

```bash
n, 3-loop time, 6-loop time
128, 1.80879, 0.296875
256, 17.4691, 2.47562
384, 64.231, 10.6901
512, 155.304, 25.5556
640, 305.552, 49.8101
768, 526.027, 85.8722
896, 858.714, 140.238

```
```
// Got help from chatgpt
We discussed this in class. It has to do with the cache blocking. You basically reduce the cache miss by breaking the matrices into smaller sub-blocks that fit into the cache, allowing the algorithm to perform multiple operations on those blocks before moving on to the next block. This reduces the number of times data needs to be loaded from memory. For bigger projects with stronger processing power, they can grab the whole matrix as one whole block.

In the blocked approach, once a block of A and B are loaded into the cache, they are reused multiple times for different calculations before being evicted. In the3-loop method, data is often reloaded multiple times because it was evicted from the cache due to poor access patterns.

```

**10. (3pt) What's the logic error in the statement "the test passed so my code is correct".**

```
Because how can we be sure that our tests are actually testing the code we are writing 

We can check this with incorrect code -> test fails
```

**11. (2pt) Prove your code in 7.1 is correct using induction theory.**

```
Base cases is true because we return 0 and 1 for f(0) and f(1)

F(k) is true. Then, F(k+1) must be true 

F(k+1)= F(k)+F(k−1)

In the iterative function, this is achieved by:
result = prev1 + prev2;
prev1 = prev2;
prev2 = result;

prev1 holds the value of F(k−1)F(k-1)F(k−1).
prev2 holds the value of F(k)F(k)F(k).
result calculates F(k+1)F(k+1)F(k+1) as F(k)+F(k−1)F(k) + F(k-1)F(k)+F(k−1).
After updating prev1 and prev2, they correctly store F(k)F(k)F(k) and F(k+1)F(k+1)F(k+1) for the next iteration.

```

**12. (5pt) Write code to help us estimate the size of stack memory in bytes.**

The stack memory is the section of memory that's used for storing local variables and making function calls. Comparing to heap memory, stack memory is limited in size and it's "machine specific", e.g. on Linux and Mac the stack size could be different. Write a code that prints out the size of stack in bytes. No loop of any kind is allowed. And there shouldn't be any use of the *new* operator. With the code, running it only once and we could get the size of the stack.

```
// Help from chatgpt

Using this code in CLion, my estimated stack size is around 2048064 bytes. That's all I was able to get to before it crashed.


#include <iostream>

void estimateStackSize(int depth, char *initialAddress) {
    char current; // Local variable to get the current stack address

    // Base case: print the estimated stack size when depth is 0
    if (depth == 0) {
        std::cout << "Estimated stack size: " << initialAddress - &current << " bytes" << std::endl;
        return;
    }

    // Recursive call with a smaller depth
    estimateStackSize(depth - 1, initialAddress);
}

int main() {
    char initial; // Local variable to get the initial stack address
    estimateStackSize(32000, &initial); // Use a smaller depth to prevent crashing
    return 0;
}



```

**Extra credit (3pt): Explain the issues in the following test code for soring algorithm. This is from a lecture demo [here](https://github.com/a-teaching-goose/2024-summer-342-demo-sorting-complexity/blob/bubble_sort/test.hpp#L75).**

```c++
        bool failed = false;
        for (int i = 0; i < size - 1; i++) {
            if (actual[i] > actual[i + 1]) {
                std::cout << "FAILED at size " << std::to_string(size) << std::endl;
                failed = true;
                break;
            }
        }
        CHECK_FAILURE(failed, expect, actual);
```

```
The problem is that you can purposely change the original data to be wrong so that the whole test can be wrong 

This is only check if the case is wrong so if the data is all 0 

Data[i] = 0 is not bigger than data[i+1] = 0 so failed will not be true even though the test clearly failed 

```

Extra credit (2pt): Explain in 5.2, why the memory leak is 40 bytes.
The code allocates an array of 10 integers in DerivedClass. 4*10 = 40 bytes 
Only the BaseClass destructor is called and it wasn’t defined correctly so the 40 bytes never got deleted
