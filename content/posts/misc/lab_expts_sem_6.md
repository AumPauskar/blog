+++
title = 'Lab expts sem 6'
date = 2024-03-23T15:34:19+05:30
tags = ["ai", "ml", "lab", "sem6", "expts", "network", "shell", "linux", "artificial intelligence", "machine learning"]
author = "Aum Pauskar"
showToc = true
TocOpen = false
draft = false
hidemeta = false
comments = false
description = "Lab experiments of semester 6, has AIML temworks and unix based network programming"
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

# Lab expts sem 6

## AIML

- Depth first search code

```py
def iterative_deepening_dfs(start, target, max_depth):
    depth = 0
    print("Depth: ", depth)
    bottom_reached = False
    while not bottom_reached and depth <= max_depth:
        result, path, bottom_reached = iterative_deepening_dfs_rec(
            start, target, 0, depth, [])
        if result is not None:
            return result
        depth += 1
        print("Increasing depth to " + str(depth), "\n")
    return None


def iterative_deepening_dfs_rec(node, target, current_depth, max_depth, path):
    print("Visiting Node " + str(node["value"]))
    if node["value"] == target:
        print("Found the node we're looking for!")
        return node, path, True
    if current_depth == max_depth:
        if len(node["children"]) > 0:
            return None, path, False
        else:
            return None, path, True
    bottom_reached = True
    for i in range(len(node["children"])):
        result, path_copy, bottom_reached_rec = iterative_deepening_dfs_rec(node["children"][i], target, current_depth + 1,
                                                                            max_depth, path + [node["value"]])
        if result is not None:
            return result, path_copy, True
        bottom_reached = bottom_reached and bottom_reached_rec
    return None, path, bottom_reached


def print_tree(node, prefix="", is_tail=True):
    print(prefix + ("└── " if is_tail else "├── ") + str(node["value"]))
    if node["children"]:
        for i, child in enumerate(node["children"]):
            print_tree(child, prefix + ("    " if is_tail else "│   "),
                       i == len(node["children"]) - 1)


tree = {
    "value": 1,
    "children": [
        {
            "value": 2,
            "children": [
                {"value": 5, "children": []},
                {"value": 6, "children": []}
            ]
        },
        {
            "value": 3,
            "children": [
                {"value": 7, "children": []},
                {"value": 8, "children": []}
            ]
        },
        {
            "value": 4,
            "children": [
                {"value": 9, "children": []},
                {"value": 10, "children": []}
            ]
        }
    ]
}

print("\nTree structure:")
print_tree(tree)

target_value = 10
print("\nTarget node:", target_value)

max_depth = 2
print("\n Max depth:", max_depth)
result_node = iterative_deepening_dfs(tree, target_value, max_depth)
if result_node:
    print("\nTarget node found:", result_node["value"])
else:
    print("\nTarget node not found in the tree.")
```

## USP

### Running a code

We shall use fedora to run most of the code. The code will be written in ANSI C and. \
To run the code, we shall use the following commands:

```shell
gedit <filename.c>
cc filename.c
./a.out
```

**Sample code**

```c
#include <stdio.h>
int main()
{
    #if __STDC__ == 0
    printf("CC is not ANSI C compliant");
    #else
    printf("%s compiled at %s %s this statement at line %d", __FILE__, __TIME__, __DATE__, __LINE__);
    #endif
    return 0;
}
```

In order to compile and run this code open a **new instance in the terminal** and execute the following commands:

```shell
cc <filename.c> -o <filename.out>
./filename.out
```

A **shorter version** to run this code is

```shell
cc <filename.c> -o <filename.out> && ./filename.out
```

This can be done for same in a c++ file. To initialte a c++ file, use the following command:

```shell
gedit <filename.cpp>
```

To compile and execute the file run the following commands:

```shell
g++ <filename.cpp> -o <filename.out>
./filename.out
```

Similarly to the c file to run the command in one single line use the following command:

```shell
g++ <filename.cpp> -o <filename.out> && ./filename.out
```

**Checking the version of posix**

```cpp
#define _POSIX_SOURCE
#define _POSIX_C_SOURCE 199309L
#include <stdio.h>
#include <unistd.h>
#include <iostream.h>

using namespace std;

int main() {
    #ifdef _POSIX_VERSION
        cout << "POSIX compliant" << _POSIX_VERSION << endl;
    #else
        cout << "POSIX version is not defined" << endl;
    #endif
    return 0;
}
```
