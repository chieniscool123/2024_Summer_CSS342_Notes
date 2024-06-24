## LECTURE 2 

### Things I am confused about 
MakeFile 
Complier 


### Code demo in lecture
```C++
#include <iostream>
#include "sorter.hpp"

int main(int argc, char **argv) {
        int array[] = {5, 4, 3, 2, 1};

    Sorter::bubble_sort(array, 5);

        for (int i=0; i<5; i++) {
                printf("array[%d] = %d\n", i, array[i]);
        }

// Dymanic Allocation
../02_use_makefile/hello_world.cpp                           
#include <iostream>
#include "sorter.hpp"

int main(int argc, char **argv) {
        int *array = new int[5]{5, 4, 3, 2, 1};

    Sorter::bubble_sort(array, 5);

        for (int i=0; i<5; i++) {
                printf("array[%d] = %d\n", i, array[i]);


```

### Things I learned 

#### VIM commands
Edit file: vi file_name
Quit : ESC -> :q
Type mode: i (Insert)
Command mode: ESC from the type mode
Save: ESC -> :w
create number line : : set number
VIM split screen : vsp file_name

#### GIT commands
git diff
git commit -am "your message here"
git push (make sure to create a token for ur password)

#### GITHUB

#### Linux Commands
show your file in a tree : tree
provides a detailed list of all files and directories, including hidden ones, in the current directory : ls -la
go to the previous directory : cd.. 
remove directory : rm -rf directory_name
check for memory leak : valgrind ./exe_file_name

#### Compiler
g++ -std=c++11 hello_world.cpp sorter.cpp -o my_executable

#### MAKEFILE (1st quiz)

CC=g++
FLAG=-Wall -std=c++11 // version
EXE=my_executable // exe file_name

all: $(EXE)

sorter.o: sorter.cpp sorter.hpp // To get sorter.o, we need to compile its .cpp and .hpp file
        $(CC) $(FLAG) -c sorter.cpp -o sorter.o

hello_world.o: hello_world.cpp // To get helloworld.o, we need to compile its .cpp file
        $(CC) $(FLAG) -c hello_world.cpp -o hello_world.o

$(EXE): hello_world.o sorter.o  // To create the executable file, we need these two files
        $(CC) $(FLAG) hello_world.o sorter.o -o $(EXE)     

clean:
        rm $(EXE) *.o

To compile:
make or make -j 4

To run:
./my_executable

to clean up
make clean

#### CMAKE
Machine will write the make file for you

cmake_minimum_required(VERSION 3.10)
project(my_executable)

set(CMAKE_CXX_STANDARD 17)

SET(CMAKE_CXX_FLAGS  "-DDEBUG -g -O0")

add_executable(${PROJECT_NAME} hello_world.cpp sorter.cpp)

SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall")

bash
# to create make file
mkdir build
cd build/
cmake ..

# to compile using makefile
make

# to run
./my_executable


#### Dynamic Allocation

#### FACB

1. Fork
2. Action ( Action Tab on GitHub to activate WorkFlow) 
3. Clone ( Clone it to your local machine via CLion) 
4. Branch



### Something to read after lecture
Question on MakeFile on first quiz 

### Reminders
- Quiz ( Due next Wednesday )
- Homeworks about going through the submission process ( Due next Sunday )

### Quiz
1. Forked
2. Create work branch
3. Check to do tab at the bottom on CLion for lists to do
4. Submit the link to your github once done

### Homework
1. Question 4 : Can turn in after deadline
2. Question 3 : Write your own test
