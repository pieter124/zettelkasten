2025-05-31 

Tags: [[linux]] [[library]] [[project]]
# **Library & Dependencies**

```
sudo apt install build-essential
sudo apt install libsdl2-dev
sudo apt install libsdl2-image-dev
sudo apt install libsdl2-ttf-dev
sudo apt install libsd2-mixer-dev
sudo apt install liblua5.3-dev
```

~~~
To compile a C++ file:
	g++ file_name.cpp 
~~~

Compile flags for C++:
- -o : Let's us set the name of the output file. After .cpp file.
- -Wall : Shows all the warnings in the .cpp file. Comes before .cpp file.
- -std=c++{version_number} : Allows us to specify the compiler version for our .cpp file. Comes before .cpp file, e.g. -std=c++17.

It becomes annoying to write all these things over again each time we have to compile our program. We can use the GNU make tool to make our lives easier.

**Header & implementation files**

We can divide a C++ program into 2 files, a file with the extension .h or .hpp (can use either but if your code base has both C and C++ files then it is good practice to use .hpp for C++ and .h for C) for header and the file with the extension .cpp for the implementation.

Example:
```cpp
int CountWordsInSentence(const char* sentence);
void ReverseString(char* str, int begin, int end);
```

Header files only contain the function "prototypes" and not the implementation.
The cpp file holds the actual body / implementation of those functions in the header files.

We have to $\text{\#include}$ in the .cpp file.

**Linking**
```cpp
#include <SDL2/SDL.h>
```
There is an error when using $\text{SDL\_Init()}$ as there is a linker error.

**C++ Compilation**
Main three phases underneath the compiler:
- **Preprocessor**
	Scans the code, parses all lines of code and looking for the $\text{\#}$ statements. These are **preprocessor directives**. The preprocessor literally includes all those contents of that header file in my source code e.g. $\text{\#ifdef WIN32}$
- **Compilation**
	Compiler parses and checks if everything makes sense. If the source code obeys the rules of the C++ syntax, if functions are being called correctly. Compiler doesn't care about the body of the function, all it cares is the function call, parameter order, etc is correct or not.
- **Linker**
	This is where we link all the implementation of the libraries we are using, the linker fetches the implementation of those libraries and bundles them together.

To solve the linker error we had, we have to change our build command. 
```cpp
g++ -Wall -std=c++17 Main.cpp -lSDL2 -o Main
```
The $\text{-lSDL2}$ links the actual implementation of the functions in the $\text{SDL2}$ library.

As we have to use a lot of dependencies / libraries, we have to link all of these in our build command. This can get tedious so we need to use Make files.

**Makefile**

```cpp
make
```

This reads a file called Makefile and executes all of the commands in it to build our program. 
Inside our makefile, we can insert a couple things called rules.
```cpp
build:
	g++ -Wall -std=c++17 src/*.cpp -lSDL2 -o gameengine
```
```cpp
run:
	./gameengine

clean:
	rm gameengine
```
Makefile needs indentation to be done with the $\text{TAB}$ character.
	
We can specify which rule to use in the command line e.g. $\text{make build \&\& make run}$
Since build is the first rule in our makefile, we can just use $\text{make}$ in the command line to build our executable.

**Updating our $\textbf{/libs}$ folder**
So SDL3 already exists and Pikuma wants to clarify what that means for our implementation, whether we need to modify everything to accustom to SDL3.

```cpp
`sdl2-config --libs --cflags`
```
This is a smart command provided by SDL we can use in our makefile build command which tells SDL to find out the linker flags we need for our program. This also means we do not have to specify the SDL2 in the include statement so we can just say $\text{\#include <SDL.h>}$

**Compiling & Testing All Dependencies**
We need to use the $\text{-I}$ flag to specify the directory to look for header files.

**References**

Pikuma's 2D Game Engine Course