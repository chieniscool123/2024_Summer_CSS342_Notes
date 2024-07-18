
### Single Choice Questions

**1. (2pt) which one below is correct. Queue**

- (D) Is FIFO "first in, first out" data structure.


**2. (2pt) Which of the following is incorrect regarding the "new" operator in C++?**

- (B) The memory allocated in a function using *new* will be released automatically when the function returns.

  
**3. (2pt) Which of the following is incorrect regarding single linked list?**
- (D) A linked list is always faster than array for insert and deleting data. // not always

**4. (4pt) Given the following code with a ListNode<T> left out, answer the following question**

```java
#include <iostream>
#include "node.hpp"

ListNode<int>* initialize_list(int n);

int main() {
    ListNode<int> *list = initialize_list(5);

    ListNode<int>*ptr = list;
    int sum = 0;
    while (ptr != nullptr) {
        sum += ptr->val;
    }

    std::cout<< sum << std::endl;

    /*
     * TODO: write code here to delete the linked list
     */
}

ListNode<int>* initialize_list(int n) {
    ListNode<int> head;
    for (int i = 0; i < n; i++) {
        auto new_node = new ListNode<int>(i);
        new_node->next = head.next;
        head.next = new_node;
    }
    return &head;
}
```

4.1 (2pt) Fix the bug in the code that cause memory issue.
```
head is declared as a local variable so it will be allocated on the heap so it will be gone and we lose the head once the function return
ListNode<int>* head = new ListNode<int>(0);

while loop is not advancing so it will continue forever
   while (ptr != nullptr) {
        sum += ptr->val;
        ptr = ptr->next;  
    }


```


4.2 (2pt) Finish the code in the TODO section as required. Make sure the code does not have no memory leak. 

```
 ptr = list;

    while (ptr != nullptr) {
        ListNode<int>* temp = ptr;
        ptr = ptr->next;
        delete temp;
    }



```


**5. (10pt) Given the following code with a bug. The Dog class is defined [here](https://github.com/a-teaching-goose/2024-summer-342-quiz-oop/blob/solution/Pets/dog.h).**

```c++
int main() {
    Dog *sam_the_dog = new Dog("Sam", 5, "Lisa");

    increase_age_by_one(*sam_the_dog);

    std::cout << sam_the_dog->get_age() << std::endl; // <- output of this line

    delete sam_the_dog;
}

void increase_age_by_one(Dog dog) {
    dog.set_age(dog.get_age() + 1);
}

```
(5pt) What's the *cout* output of the above code without any change?

```
5 because you are passing in the value for the increase_age_by_one function. So you changed the copy instead of the original 


```

(5pt) Fix the bug so it output the correct result. The fix is **only allowed in the increase_age_by_one function**. Write the fixed function increase_age_by_one. After the fix, the logic should be correct (age of dog passed in as parameter incremented) without memory leak.

```
I changed it so that you are now passing in the reference 
void increase_age_by_one(Dog& dog) {
    dog.set_age(dog.get_age() + 1);
}

```


**6. (5pt) Given this code from [one of our quizes](https://github.com/a-teaching-goose/2024-summer-342-quiz-stack-queue/blob/solution/queue.hpp#L54) about circular queue:**
```c++
 T dequeue() override {
        if (num_of_elements == 0) {
            throw std::exception();
        }
        T val = data[front_idx];
        front_idx = (front_idx + 1) % capacity;  // <- explain this line
        num_of_elements--;
        if (num_of_elements == 0) {
            front_idx = end_idx = -1;
        }
        return val;
    }
```

Explain what the line with a comment does with example when 
- front_idx = 5, capacity = 6
- front_idx = 4, capacity = 6

 front_idx = (front_idx + 1) % capacity;  
 // This line basically move the position of the front_idx toward its next removal. 
 front_idx = 5, capacity = 6. front_idx + 1 = 6, 6%6 = 0. So the next removal index will be 0
 front_idx = 4, capacity = 6. front_idx + 1 = 5, 5%6 = 5. So the next removal index will be 5

 

```



```


**7. (10pt) In the following code, test is failing.**

```c++
#include <iostream>

class Array {
private:
    int *data;
    int size;
public:

    Array(int size) : size(size) {
        data = new int[size];
    }

    ~Array() {
        delete data;
    }

    int &operator[](int i) { return data[i]; } // 
};

#define ASSERT_EQUAL(expect, actual) \
    if ((expect) != (actual)) { \
        printf("Test failed. Expecting %d. Actual %d.\n", (expect), (actual)); \
    } else { \
        printf("Test passed.\n"); \
    }

#define SIZE 10

int main() {
    Array array_1(SIZE); // size = 10
    int expect = 0; 
    for (int i = 0; i < SIZE; ++i) {
        int val = i * 100; // val will be equal to 0 - 900
        array_1[i] = val; // array_1[0-9] = 0 - 900
        expect += val;  // expect = 0 + 100 +..900
    }

    Array array_2(array_1);
    for (int i = 0; i < SIZE; ++i) {
        int val = (i + 1) * 200;
        array_2[i] = val;
        expect += val;
    }

    int actual = 0;
    for (int i = 0; i < SIZE; ++i) {
        actual += (array_1[i] + array_2[i]);
    }

    ASSERT_EQUAL(expect, actual);
}
```

(8pt) Explain why the test fails and write code to fix it. 
```
Tet failed because of the line below. You are making a shallow copy of the data ptr. Both array share same memory location 
Array array_2(array_1);

Here is how I would fix it :

1. Adding a new copy constructor in the Array class
  Array(const Array &other) : size(other.size) {
        data = new int[size];
        for (int i = 0; i < size; ++i) {
            data[i] = other.data[i];
        }
    }




```

(2pt) The given code, with any bug fix, also fails memory check.

<img width="55%" alt="image" src="https://github.com/user-attachments/assets/f840c71a-a1e9-4dad-9e78-b53bfe364666">

Explain the reason of the memory issue.
```
your destructor is wrong. You only deleting basically the head. and not what followed 
should be
 ~Array() {
        delete[] data;
    }
```

**8. (5pt) What is the output of the following program?**
```c++
#include <iostream>
template<typename T>
T Max(T a, T b) {
   return a < b ? b : a; // return the bigger value 
}

int main () {
   int i = 12;
   int j = 30;
   std::cout << "Max(i, j): " << Max(i, j) << std::endl; 

   float f1 = 2.5;
   float f2 = -20.7;
   std::cout << "Max(f1, f2): " << Max(f1+f2, f1-f2) << std::endl; 
```
```

Max(i, j): 30
Max(f1, f2): 23.2


```

**9. (5pt) Convert the folowing class to a template class so it takes a type T instead of float. Write the complete code in the answer.**
```c++
#include "math.h


class ComplexNumber {
    float x;
    float y;
public:
    ComplexNumber(float x, float y) : x(x), y(y) {}
    float distance() { return sqrt(x*x + y*y);}
};
```

```
template <typename T>
class ComplexNumber {
    T x;
    T y;
public:
    ComplexNumber(T x, T y) : x(x), y(y) {}
    T distance() { return sqrt(x*x + y*y);}
};


```

**10. (15pt) Given the following code:**
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

class SingleLinkedList {
private:
    ListNode *head;
public:
    SingleLinkedList() {
        head = new ListNode();
    }
    ~SingleLinkedList();
    int mid_node();
    int nth_to_last(int);
};
```

Implement the nth_to_last(n) member function that returns the value of the ith node from the end of a linked list.

For example, for a linked list 1->2->3->4->5->N
```
when n is 0, nth_to_last returns 5
when n is 1, nth_to_last returns 4
when n is 2, nth_to_last returns 3
When n is 8, what should nth_to_last do?
```
Note that input list is not always sorted. 

(10pt) Implement the nth_to_last function. **5pt extra credit** if your code only travels through the linkedlist no more than one time.
```c++

// Got some help from chatgpt with how the two use the ref_ptr to track how many nodes there are in the linkedlist
int SingleLinkedList::nth_to_last(int n) {

 if (n < 0) {
        throw std::invalid_argument("n must be bigger than 0");
    }

    ListNode* main_ptr = head->next; 
    ListNode* ref_ptr = head->next;  

    int count = 0;
    while (count < n) {
        if (ref_ptr == nullptr) {
            throw std::out_of_range("not enought nodes in the linkedlist");
        }
        ref_ptr = ref_ptr->next;
        count++;
    }

    while (ref_ptr != nullptr && ref_ptr->next != nullptr) {
        main_ptr = main_ptr->next;
        ref_ptr = ref_ptr->next;
    }

    return main_ptr->val;
}


}
```

(5pt) Discuss how you would handle edge cases, for example, when list has only 3 nodes but n is 8. 
```
right here. So for example, you will have 3 nodes
1st run : count = 0 < 8 so it will run 
2nd run: count = 1 < 8 so it will run
3rd run: count =2 < 8. it will run
4th run. count = 3. ref_ptr = null ptr so it will not run
   int count = 0;
    while (count < n) {
        if (ref_ptr == nullptr) {
            throw std::out_of_range("n is greater than the number of nodes in the list.");
        }
        ref_ptr = ref_ptr->next;
        count++;
    }


```


**11. (5pt) What's a unit test? If we ourselves write both function code and test, and the test we write will pass at last, what's the point of having any test?**
```
To isolate a specific section of the code for testing. It is to make sure that each unit of the software is performance as exepected.

Just because you write the function does not mean it will perform as expected from the test.


```

**12. (5pt) Why is it not a good idea to use any kind of printing for software testing?**
```
It is very complicated and time consume to write any kind of printing for software testing
It is also very hard to read due to the clutter information in the terminal

```

**13. (10pt) Given the following class for rubber duck**
```
class RubberDuck {
public:
    void talk(const std::string &words);

    std::string walk(int &steps) {
        std::string msg;
        for (int i = 0; i < steps; i++) {
        msg += "walk(step " + std::to_string(i) + ")!\n";
        }
        steps += 100;
        return msg;
    }

    RubberDuck(const std::string &name) : name(name) {}

    std::string &get_name() {
        return name;
    };

private:
    std::string name;
};

```

13.1 (5pt) Walk walk walk

```c++
RubberDuck duck("Tim");
int steps = 10;
std::string msg = duck.walk(steps);
std::cout << "duck walk returns '" << msg << "'\n"; 
std::cout << "duck " + duck.get_name() + " walked " + std::to_string(steps) + " steps\n";
```

Here's part of the output
```
duck Tim walked 110 steps
```

Explain why its 110 steps instead of 10 steps printed.
```
std::string msg = duck.walk(steps);
the walk method is taking in the reference to steps and modify 'steps' directly.
It is in this line right here  steps += 100;



```

13.2 (5pt) Find the memory issue (not necessarily leakage).

```c++
auto *duck = new RubberDuck("Jerry");
std::string &duck_name = duck->get_name();
std::cout << "Duck's name is " << duck_name << "\n";
delete duck;
std::cout << "Duck's name is " << duck_name << " after delete\n";
```
And any problem (hint: memory related) with this code?
```
I used chatgpt for this problem
I learned something called a dangling reference
So the duck object is deleted but the duck_name is still holding a reference to the memory location where the name was stored.



```

**14. (15pt) Given the following color class**

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

    // TODO: add your code here

private:
    int color;
};
```

(8pt) Add to the Color class with a function that allows adding basic color (RED, GREEN, BLUE) together using "+"
```
// Overloading operator + 
 Color operator+(Color const &another_color) const {
        switch (color) {
            case RED:
                switch (another_color.color) {
                    case GREEN:
                        return Color(YELLOW);
                    case BLUE:
                        return Color(MAGENTA);
                    case RED:
                        return Color(RED);
                    default:
                        return Color(UNKNOWN);

                }
            case GREEN:
                switch (another_color.color) {
                    case GREEN:
                        return Color(GREEN);
                    case BLUE:
                        return Color(MAGENTA);
                    case RED:
                        return Color(YELLOW);
                    default:
                        return Color(UNKNOWN);
                }
            case BLUE:
                switch (another_color.color) {
                    // notice a different way to return object
                    case GREEN:
                        return {CYAN};
                    case BLUE:
                        return {BLUE};
                    case RED:
                        return {MAGENTA};
                    default:
                        return Color(UNKNOWN);
                }
        }
        return Color(WHITE);
    };



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
    ASSERT_EQ(cyan, blue + green);
}
```

(7pt) Write down how you would test your function as thorough as possible. You can write code or text description or both for your test plan.
```
    ASSERT_EQ(red, red + red);
    ASSERT_EQ(magenta, red + blue);

    ASSERT_EQ(cyan, green + blue);
    ASSERT_EQ(yellow, green + red);
    ASSERT_EQ(green, green + green);

    ASSERT_EQ(blue, blue + blue);
    ASSERT_EQ(cyan, blue + green);
    ASSERT_EQ(magenta, blue + red);




```

**15. (5pt) Explain why this [descructor](https://github.com/a-teaching-goose/2024-summer-342-quiz-oop/blob/solution/Pets/pet.h#L35) needs to be "virtual". If it's not virtual, what would be the consequence?**

```
If it not declared as virtual then when you call delete pet, only the destructor of the Pet class is called, not the destructor of the Dog class.
To clean up properly and manage your resources. you need to declare your base class "pet" as virtual.


```

**(2pt) Extra Credit 1**

Explain how this makefile works to generate the executable:

```makefile
CC=g++
FLAG=-Wall -std=c++11 
EXE=my_executable

all: $(EXE) 

sorter.o: sorter.cpp sorter.hpp
	$(CC) $(FLAG) -c sorter.cpp -o sorter.o

hello_world.o: hello_world.cpp 
	$(CC) $(FLAG) -c hello_world.cpp -o hello_world.o

$(EXE): hello_world.o sorter.o
	$(CC) $(FLAG) hello_world.o sorter.o -o $(EXE) 

clean:
	rm $(EXE) *.o
```

```
To create the exe file you need hello_world.o and sorter.o 
But you need the hello_world.cpp and sorter.cpp to create the .o file so you basically keep moving back until you got all the file needed to create the exe file 


```

**(2pt) Extra Credit 2**
In the lecture, the teacher proposed an idea that unit test can be treated as a *contract* between requirements and deliverables. Explain this idea especially why "bare minimum" was mentioned in that part of the lecture.
```
You said you should never said my code should be correct. Only say my code passed all the tests which is the basic requirements. Passing the tests can be seen as an acctaple results. 


```

**(2pt) Extra Credit 3**
In the lecture, the teacher explained why allowcating memory from heap is potentially slower than from stack. What was the reason for this performance difference mentioned in lecture?

```
 The problem have to do with fragmentation and the need to find appropriate blocks of memory dynamically
Let's use array as an example  The system must find a block of memory large enough to hold the array. The system might need to locate a suitable space, making it slower than stack allocation.

```

**(2pt) Extra Credit 4**

What is the fix for [this bug](https://github.com/a-teaching-goose/2024-summer-342-quiz-oop/blob/main/Pets/dog.h#L18) and why?

```
 it takes the owner parameter by non-const reference.

   Dog(const std::string &name, int age, std::string &owner) : Pet(name, age) {
        this->owner = owner;
    };

Where the constructor declared it as a const refer
Dog::Dog(const std::string &name, int age, const std::string &owner,
         Pet **friends, int num_of_friends) : Dog(name, age, owner) {
    if (num_of_friends <= 0) {
        return;
    }

So just add const infront of owner
 Dog(const std::string &name, int age, const std::string &owner) : Pet(name, age) {
    this->owner = owner;
}


```
