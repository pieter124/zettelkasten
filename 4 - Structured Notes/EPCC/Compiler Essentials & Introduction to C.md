2025-06-17 

Tags:  [[programming]] [[compilation]] [[operating systems]]

# **Introduction to C** 

**Compilation Essentials**

Compiler we use is GCC (GNU Compiler Collection).

**How does it work?**

Compile commands:
```
// Compile into 'binary_name' executable/assembler output.
gcc -o binary_name source1.c source2.c

-o flag : able to set the name of the output machine code file.

// The normal way to compile and execute.
gcc source.c
./a.out

// To change the name of the executable to main and put it int the directory my_dir
gcc -o my_dir/main main.c

// Multi file compilation
Must list all source files, not header files.

The compiler does lexical analysis:
it works by looking at each space-separated block. Comparing them against a table of regular expression and indicates the purpose of each block (i.e token).

It also does syntax analysis:
It compares each series of tokens against a table listing possible combinations and maps each to corresponding statement.

It does semantic analysis:
Declaring an int and assigning 123 to it for example: OKAY.
Assigning 456 to it: OKAY.

The most important for HPC's are optimization analysis:
It analyses for potential optimizations and applies optimisations deemed suitable.

```

**Compiler optimisations**

Loop optimisations include:
![[Pasted image 20250617142635.png]]
General optimisations include:
![[Pasted image 20250617142844.png]]

Interpreted languages only benefit from a subset of these optimisations which is why compiled languages are or can be orders of magnitude faster.

Compilers typically offer multiple levels of optimisations, You can use different flags to specify the optimisation 'level'.

Why would you use -O0 as a flag? Useful to check for incorrectness.

Why would you use anything other than -O3? It has unsafe compiler optimisations, which impose more preconditions in order to leverage more room for optimisation. In addition, it can significantly increase compilation time.

Why ever use -O1 instead of -O2? Both are safe but -O2 may increase the amount of time necessary for compilation. In addition, it can also result in a greater loss of information for debugging.

**Modular compilation**
In GCC, you must pass the "-c" flag to ask for production of object files.
```
// Compile the source file main.c to an object file
gcc -o main.o -c main.c

// Compile the source file my_func.c to an object file
gcc -o my_func.o -c my_func.c

// Produce the executable by linking object files.
gcc -o main main.o my_func.o
```

Two-phase approach allows you to develop libraries and plug-ins.
- You write an interface, with function declarations, which act as the Application Programming interface. 
- You implement their definitions. 
- You compile them.

**Important Flags**

```
When using an #include statement, the compiler must find the corresponding file.
Locations listed as "include paths" will be visited to find the file specified.
Adding a given location can allow you to use customised locations.
Use the flag -I, followed with location to add.

Example:
Your program needs my_func.h from a separate program, located at /home/user123/my_includes
To add this path, add the following flag to the compilation command:
-I/home/user123/my_includes 

(There is no space between -I and the location.)

Adding a library path
Example:
-L/home/user/my_libs
Notation is -L instead of -I.

Example:
Once the compiler knows where to look for the libraries, you can specify the libraries to fetch using the -l flag. For example, to load the library libhpc.so:
-lhpc

Careful: You only pass the root name of the library ("hpc") and you prefix it with -l, not the extension of the "lib" prefix.

So -L is to add a library path, -l is to add the library itself.

// Defines

Passing -DMY_CONST=123 to the compilation command will define a constant named MY_CONST and assign it value 123. Defines can simply declare a constant without assigning a value to it. You use -D to handle at compiler level.

You can use this to:
- Trigger a debug mode in your code
- Change a datatype
- Control parallelism options
- ...

Compilers can also provide more guidance by being more restrictive about the checks it performs.
- Undefined variables
- Unused variables
- Unused return values
- NULL pointers
- Statements after return
- Branches never taken
- Returned value not used

Tip:
Keep -Wall on all the time. It enables a broad range of warning messages.
-Wextra enables additional warnings.

To turn all warnings into errors right away, to prevent compilation, use -Werrors. To turn errors into fatal errors, to have compilation stop after the first error, use -Wfatal-errors.

To specify a compiler version for C, use the flag -std=X, where X has one of the values below.
For C:
c89, c99, c11, c17, c23 to name a few.
For C++:
c++98, c++99, c++11, c++14, c++17, c++20, c++23 to name a few.

Tip
Familiarise yourself with common error messages.
```


**Preprocessor Directives**

Preprocessor directives are handled before your actual code is even parsed.
You can find:
```
#include : copy/paste the content of the file specified at the location of the #include.

#define : specifies that a given constant exists, and optionally assigns it a value. 
(This is useful for turning on debug-specific code).

#ifdef /ifndef / #else / #endif : executes portions of the code only if a constant is defined (#ifdef) or not defined (#ifndef). This is useful for inclusion guards or hardware-specific code.

When doing shared memory parallelism in OpenMP, you will see directives such as:
#pragma omp parallel
#pragma omp for
#pragma omp barrier
```

**What they do not like**

Anything that hinders a compiler's vision at compile-time makes their life harder to optimise code. Typically:
- Pointer jumping for memory locations (i.e. a pointer on a pointer on a pointer..)
- Pointer jumping for routines (i.e. function pointers)
- Runtime-determined information
- Pointer aliasing (i.e. can two pointers point to the same memory location?)
- Parallelism /  non-determinism

**Introduction to C** 
```
This is all relative to C.
// Variables

Variable names can contain underscore, no other special characters.

float is single-precision, IEEE standard.

double is double-precision floating point number, uses twice the memory than a float.

// int main explanation

Whenever a program is run, it looks specifically for a function called main which is the startpoint for every program. The C compiler always looks for this function.

// Shell 
All shell commands are found at $PATH.

// Functions
All arguments are compulsory; there are no optional arguments.
Functions cannot be overloaded.

// Pointers

Pointers can be used to pass variables by reference to functions. It essentially allows the original instance of the variable, not a copy of it.

// Arrays
Dynamically allocated arrays
Their size is not required until runtime. Allocated on the heap, where the corresponding memory is not deallocated until explicitly freed by the developer,

It is good practice to cast it back to a pointer on your type.
int* my_array = (int*) malloc(sizeof(int) * 10);

// Multidimensional arrays

It is said to be "row-major order". It means that the elements in the same row are consecutive in memory. Regardless of the dimensions, this means that elements in the rightmost dimension are consecutive in memory.

// Structures

Example struct:

struct Person {
    float weight;
    float height;
};

If you have a pointer on a structure, say in a function, you can deference it, then access the members. This is quite cumbersome so instead of doing all that you can use the arrow '->' to achieve the same result.

The struct keyword in struct person can be redundant.
You can "rename" the struct person in person_t using typedef. Only a syntactic change.

Example:
typedef struct person {
	float weight;
	float height;
} person_t

// Function declarations

A function declaration:
void my_func();

A function definition:
void my_func() {

}

// Multi-file structure

Source: Contains function definitions. Uses ".c" file extension.
Header: Contains function declarations. Uses ".h" file extension.

Use the #include preprocessing directive so the compiler knows where to look.

Preprocessor directives are instructions given to the preprocessor, which treats the source code before the compiler reads it.

They have three main uses:
- Include other files (c.f.: #include) 
- Exclude certain portions of code from compilation.  
- Automatically replace certain occurrences with literals.

Preprocessor directives as inclusion guards
#ifndef SOME_NAME
    #define SOME_NAME
    void my_function();
#endif

The first time this header is included, the symbol name SOME_NAME does not exist.
The ifndef directive, which stands for "if not defined", checks that the symbol SOME_NAME does not exist. It is the case here indeed, so it executes the block associated. The define declares the symbol, and the function is declared in the line that follows. From now on, including this header will have no effect because the symbol SOME_NAME is now defined and the check done by the directive ifndef will systematically fail.

Defines can also assign a value to a symbol.
Each occurence of that symbol will be replaced with the value provided.
This is useful to easily change the size of statically allocated arrays passed through functions without having to update all values one by one manually.

void* function returns a void pointer (raw memory pointer).

// Good Practice

For constants, use exclusively uppercase letters, and usually exclusive lowercase letters for anything else. Use underscores when needed.

Stay consistent with loop indentation and curly braces placement.

// This is a single line comment

/* Here is a 
multi-line comment */

/**  Here is a 
documentation comment **/

Learn Doxygen. Good for interviews.

```

**Key Ideas:**
Do not compile header files, only compile source files.
Header files are used for better structure of code.
Use gcc -O0 for quick testing for incorrectness.
It is good practice to cast the return type from malloc to the type of pointer you declared.

**Further Reading (questions & resources)**:
Compiler optimisation is a wide area.
- superoptimisers
- synthesis-based approaches
- stochastic superoptimisation
- ML-aided superoptimisation
Compilers have front-end(s) and back-end(s).
Compilers rely on intermediate representation (IR).
Programming language grammar syntax (CFG, BNF).


**References**
*EPCC HPC Summer School*
**Lecturers: William Lucas
