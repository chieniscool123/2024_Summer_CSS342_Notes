### Reference
#### Definition: An alias for an existing variable.
#### Memory: Shares the same memory address as the original variable.
#### Modification: Changes to the reference affect the original variable.
#### Syntax: int& ref = original;
#### Usage: Avoids copying large objects, useful for function parameters and modifying arguments directly.

### Pointer
#### Definition: A variable that stores the memory address of another variable.
#### Memory: Stores the address of the target variable, can point to different variables.
#### Modification: Use * to dereference and access/modify the value at the pointed address.
#### Syntax: int* ptr = &original;
#### Usage: Dynamic memory allocation, arrays, data structures, and for passing variables to functions efficiently.

### Copy
#### Definition: A new variable with the same value as another variable.
#### Memory: Has its own separate memory location.
#### Modification: Changes to the copy do not affect the original variable.
#### Syntax: int copy = original;
#### Usage: When an independent copy of a variable is needed

### Example

#### Pass in by reference
![image](https://github.com/chieniscool123/2024_Summer_CSS342_Notes/assets/100248105/7abbe15f-3452-476d-8b81-495df4127217)

#### Passing the Address of a Variable
![image](https://github.com/chieniscool123/2024_Summer_CSS342_Notes/assets/100248105/75c2103f-1bc0-4365-bddc-1be9ad6c79ca)

#### Passing a Pointer Variable Directly

![image](https://github.com/chieniscool123/2024_Summer_CSS342_Notes/assets/100248105/3f499879-ec26-47bb-93fb-05084d59b3fe)



#### Basic Pointer Operations
    int main() {
    int a = 10;       // Declare an integer variable 'a'
    int* ptr = &a;    // Declare a pointer 'ptr' and assign it the address of 'a'

    std::cout << "Initial value of a: " << a << std::endl;        // Outputs: 10
    std::cout << "Address of a: " << &a << std::endl;             // Outputs: address of 'a'
    std::cout << "Value of ptr: " << ptr << std::endl;            // Outputs: address of 'a' (same as above)
    std::cout << "Value pointed to by ptr: " << *ptr << std::endl; // Outputs: 10 (value of 'a')

    *ptr = 20;  // Modify the value of 'a' through the pointer

    std::cout << "New value of a: " << a << std::endl;            // Outputs: 20
    std::cout << "Value pointed to by ptr: " << *ptr << std::endl; // Outputs: 20 (same as new value of 'a')

    return 0;
}

#### Basic Reference Operations

    int main() {
     int b = 30;      // Declare an integer variable 'b'
     int& ref = b;    // Declare a reference 'ref' to 'b'

    std::cout << "Initial value of b: " << b << std::endl;  // Outputs: 30
    std::cout << "Value of ref: " << ref << std::endl;      // Outputs: 30

    ref = 40;  // Modify the value of 'b' through the reference

    std::cout << "New value of b: " << b << std::endl;  // Outputs: 40
    std::cout << "Value of ref: " << ref << std::endl;  // Outputs: 40 (same as new value of 'b')

    return 0;
}

####  Pointers and References Together


    int main() {
    int c = 50;       // Declare an integer variable 'c'
    int* ptr = &c;    // Declare a pointer 'ptr' and assign it the address of 'c'
    int& ref = c;     // Declare a reference 'ref' to 'c'

    std::cout << "Initial value of c: " << c << std::endl;         // Outputs: 50
    std::cout << "Value pointed to by ptr: " << *ptr << std::endl; // Outputs: 50
    std::cout << "Value of ref: " << ref << std::endl;             // Outputs: 50

    *ptr = 60;  // Modify the value of 'c' through the pointer

    std::cout << "New value of c: " << c << std::endl;             // Outputs: 60
    std::cout << "Value of ref after *ptr = 60: " << ref << std::endl; // Outputs: 60

    ref = 70;  // Modify the value of 'c' through the reference

    std::cout << "New value of c: " << c << std::endl;             // Outputs: 70
    std::cout << "Value pointed to by ptr after ref = 70: " << *ptr << std::endl; // Outputs: 70

    return 0;
}

#### Dynamic Memory Allocation with Pointers

    #include <iostream>

    int main() {
    int* d = new int;  // Dynamically allocate memory for an integer
    *d = 80;           // Assign the value 80 to the allocated memory

    std::cout << "Value of d: " << *d << std::endl;  // Outputs: 80

    delete d;  // Free the allocated memory
    d = nullptr; // Good practice to set the pointer to nullptr after deletion

    return 0;
}

#### Arrays with Pointers

    #include <iostream>

    int main() {
    int arr[3] = {90, 100, 110};  // Declare an array of integers
    int* ptr = arr;               // Pointer to the first element of the array

    for (int i = 0; i < 3; ++i) {
        std::cout << "Value of arr[" << i << "]: " << arr[i] << std::endl;  // Outputs: 90, 100, 110
        std::cout << "Value pointed to by (ptr + " << i << "): " << *(ptr + i) << std::endl;  // Outputs: 90, 100, 110
    }

    return 0;
}

#### POINTERS AND REFERENCE PARAMETER AND FUNCTION CALLS

### PARAMETER
![image](https://github.com/user-attachments/assets/ac95f0ab-a71f-4d39-9875-0d9dc3d99853)

### FUNCTION CALLS
![image](https://github.com/user-attachments/assets/b3db84af-a870-4b11-bf8f-4d8ce4c898be)





