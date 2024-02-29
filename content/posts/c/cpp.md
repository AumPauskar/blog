+++
title = 'Cpp'
date = 2024-02-26T11:43:37+05:30
tags = [""]
author = "Me"
showToc = true
TocOpen = false
draft = true
hidemeta = false
comments = false
description = "Desc Text."
disableShare = false
disableHLJS = false
hideSummary = false
searchHidden = true
ShowReadingTime = true
ShowBreadCrumbs = true
ShowPostNavLinks = true
ShowWordCount = true
ShowRssButtonInSectionTermList = true
UseHugoToc = true
[editPost]
    URL = "https://github.com/AumPauskar/blog/content/posts/"
    Text = "Suggest Changes"
    appendFilePath = true
+++

# Object oriented programming using C++

## Introduction
C++ is a general-purpose programming language created by Bjarne Stroustrup as an extension of the C programming language, or "C with Classes". The language has expanded significantly over time, and modern C++ now has object-oriented, generic, and functional features in addition to facilities for low-level memory manipulation. It is almost always implemented as a compiled language, and many vendors provide C++ compilers, including the Free Software Foundation, Microsoft, Intel, and IBM, so it is available on many platforms.

### Hello world script
```cpp
#include <iostream>
using namespace std;

int main() {
    cout << "Hello, World!" << endl;
    return 0;
}
```

Components of this script:
- `#include <iostream>`: This is a header file that allows us to use the input and output functions of C++.
- `using namespace std;`: This line tells the compiler to use the std namespace. The std namespace includes many of the C++ Standard Library functions.
- `int main()`: This is the main function of the program. Every C++ program must have a main function. The execution of the program starts and ends in the main function.
- `cout << "Hello, World!" << endl;`: This line is used to print the text "Hello, World!" to the screen.
- `return 0;`: This line terminates the main function and returns the value 0.

### Similarity to C
C++ is a superset of C, and it is largely compatible with C. Any legal C program is a legal C++ program. C++ is a "better C" in the sense that it is a more effective and flexible language for writing software at the cost of being more complex. C++ is a "better C" in the sense that it is a more effective and flexible language for writing software at the cost of being more complex.