
### What is keyword "virtual "
#### virtual is used to enable polymorphism, allowing you to call derived class methods through a base class pointer or reference.

### What is a Virtual Function:
#### A virtual function is a function in a base class that you expect to be redefined in derived classes. When a function is declared as virtual in the base class, it tells the compiler to support dynamic (or late) binding on this function.
### Example 

#### Basic Virtual Function
    #include <iostream>

    class Animal {
    public:
    virtual void play() { // Virtual function
        std::cout << "Animal plays" << std::endl;
    }
    };

    class Cat : public Animal {
    public:
    void play() override { // Override the virtual function
        std::cout << "Cat plays" << std::endl;
    }
    };

    int main() {
    Animal* animalPtr = new Cat(); // Base class pointer pointing to derived class object
    animalPtr->play(); // Calls Cat's play function

    delete animalPtr; // Clean up
    return 0;
}

### Summary
#### Virtual Functions: Allow derived classes to override functions in a way that enables dynamic binding.
#### Polymorphism: Enables calling derived class methods through base class pointers or references.
#### Dynamic Binding: The actual method that gets called is determined at runtime, based on the type of the object being pointed to or referenced, not the type of the pointer or reference.

#### ![image](https://github.com/chieniscool123/2024_Summer_CSS342_Notes/assets/100248105/f6e1b309-32fb-41d9-9df5-b730e7f0021e)

#### ![image](https://github.com/chieniscool123/2024_Summer_CSS342_Notes/assets/100248105/676c4fd1-13e2-4d90-81d1-2f2965fd8326)

