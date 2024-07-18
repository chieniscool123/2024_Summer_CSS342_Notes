## SAMPLE
## SAMPLE
## SAMPLE
## SAMPLE
## SAMPLE
## SAMPLE

# 2024 Summer UWB CSS 342(A) Midterm Exam

### "Single Choices"

**Queues**

- (A) are a "first in, first out" data structure // This is correct 
- (B) are a random access data structure // You can't not randomly access it
- (C) cannot be implemented using linked lists // Yes you could
- (D) are a fixed size data structure // Linked List implementation of it doesn't have to be fixed

**. Explain what issue is with the following code?**
```c++

// add(int) increment and returns the parameter value by 1
1. Oringinal
int* add(int value) { // Pass in value. Return a pointer to an int
  value = value + 1; // Changing the copy value 
  return &value; // Returning the reference to the copy 
}

2. Fixed
int * add(int *value) {
*value +=1;
return value;
}
```
## Implementation 
![image](https://github.com/user-attachments/assets/b87878b8-ca1b-4c0c-8f11-8b868d076a6c)


**In the following code**

```c++
class Array{
  int* data;
public:
  int size;
  Array(int size) : size(size) {
          data = new int[size];
  }
  int &operator[](int i) { return data[i]; }
  ~Array() { delete data; } Should be delete[]data;
};

int arrayMultiplication(Array array) {
    int sum = 1;
    for (int i=0; i<array.size;i++) {
        sum *= array[i];
    }
    return sum;
}
```

any problem with memory?
```
 Should be delete[]data;


```

**Convert the folowing class to a template class so it takes a type T instead of float.**
```c++
#include "math.h

1. Original
class ComplexNumber {
    double x;
    double y;
public:
    ComplexNumber(double x, double y) : x(x), y(y) {}
    double distance() { return sqrt(x*x + y*y);}
};

2. Fixed
template <typename T>
class ComplexNumber {
    T x;
   T y;
public:
    ComplexNumber(T x, T y) : x(x), y(y) {}
    T distance() { return sqrt(x*x + y*y);}
};
```
```



```

**Given the following code:**
```c++
class ListNode {
    friend class SingleLinkedList;
private:
    int val;
    ListNode *next;
public:
    ListNode() : next(nullptr) {}
    ListNode(int val) : val(val), next(nullptr) {}
};
```

Implement the 3rd_to_last(n) function that returns the value of the 3rd node from the end of a single linked list.

For example, for a linked list 5->3->2->1->4->nullptr, the 3rd from last is 2

Note that input list is not always sorted. 

Implement the 3rd_to_last function. **5pt extra credit** if your code only travels through the linkedlist no more than one time.
```c++
int 3rd_to_last(ListNode * head) {




}
```



**What's a unit test? If we ourselves write both function code and test, and the test we write will pass at last, what's the point of having any test?**
```



```


**Given the following class for rubber duck**
```
class RubberDuck {
public:
    void talk(const std::string &words);

    std::string walk(int &steps) {
        std::string msg;
        for (int i = 0; i < steps; i++) { // Passed in 10
        msg += "walk(step " + std::to_string(i) + ")!\n";
           }
        steps += 100; // steps is now 110 since we passing in the reference
        return msg;
      // msg = walk(step + 0 )
      // msg = walk(step+1)
      ...
      //msg = walk(step+9)
    }

    RubberDuck(const std::string &name) : name(name) {}

    std::string &get_name() {
        return name;
    };

private:
    std::string name;
};

```

**What's the outpout of the following code?*** 

```c++
RubberDuck duck("Tim");
int steps = 10;
std::string msg = duck.walk(steps); // Called the methods passing in a reference to 'steps' so 'step' is now 110
std::cout << "duck walk returns '" << msg << "'\n"; 
std::cout << "duck " + duck.get_name() + " walked " + std::to_string(steps) + " steps\n";
```

Here's part of the output
```
duck Tim walked 110 steps
```

Explain why its 110 steps instead of 10 steps printed.
```
// Called the methods passing in a reference to 'steps' so 'step' is now 110 after the method is fininshed 


```

**Given the following color class**
```c++
#define RED 0
#define GREEN 1
#define BLUE 2
#define YELLOW 3
#define MAGENTA 4
#define CYAN 5
#define WHITE 6

class Color {
public:

    // constructor
    Color(int color);

    // equality
    bool operator==(const Color &rhs) const {
        return color == rhs.color; 
    }

    // exam: add your code here

private:
    int color;
};
```

(10pt) Add to the Color class with a function that allows adding basic color (RED, GREEN, BLUE) together using "+"
```
Color opearator+(Color &colors) {
switch (color) {
case Red :
  switch (colors.color) {
      case Green:
          return Color(Yellow) ; 

} 



```

Upon finish, the following test should pass:
```c++
TEST(color, simple) {
    Color red(RED);
    Color blue(BLUE);
    Color green(GREEN);
    Color cyan(CYAN);
    Color yellow(YELLOW);
    Color magenta(MAGENTA);

    ASSERT_EQ(yellow, red + green);
    ASSERT_EQ(magenta, RED + BLUE);
    ASSERT_EQ(cyan, blue + green);
}
```


**Explain why it's a good idea to declare base class destructor as "virtual"**
```



```
