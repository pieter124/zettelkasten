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

We can divide a C++ program into 2 files, a file with the extension .h for header and the file with the extension .cpp for the implementation.



**References**

Pikuma's 2D Game Engine Course