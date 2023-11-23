+++
title = 'Basic DSA algorithms using C'
date = 2023-11-16T10:38:34+05:30
draft = false
+++

# A complete guide ds

## Termwork 1 - Infix evaluation
### Algorithm
1. Create an empty stack (operandStack) to store operands and an empty stack (operatorStack) to store operators.
2. Initialize a variable (result) to store the final output
3. Iterate through each character of the infix expression.
4. If the current character is an operand, add it to the operandStack.
5. If the current character is an operator, pop operators from operatorStack and add them to operandStack until an operator with lower precedence is found. Then push the current operator onto operatorStack.
6. If the current character is an opening parenthesis, push it onto operatorStack
7. If the current character is a closing parenthesis, pop operators from operatorStack and add them to operandStack until an opening parenthesis is found.
8. Repeat steps 3-7 for all characters of the infix expression.
9. Once all characters have been processed, pop any remaining operators from operatorStack and add them to operandStack.
10. Evaluate the final expression in operandStack and return the result.

### IO
```bash
 * ➜  programs git:(ds) ✗ gcc tw1.c -lm && ./a.out
 * Output 1
 * Enter the infix expression to evaluate: 5+7-4+3
 * 11
 * 
 * Output 2
 * Enter the infix expression to evaluate: 6+6
 * 12
 * 
 * Output 3
 * Enter the infix expression to evaluate: 4*6^2
 * 256
```
### Applications
1. Expression Evaluation: Stacks are commonly used in the evaluation of mathematical expressions, such as infix and postfix expressions. By using a stack, one can easily convert an infix expression to postfix and then evaluate the postfix expression. This is because stacks provide a last-in-first-out (LIFO) data structure, which is well suited for this type of evaluation.
2. Undo/Redo functionality: Stacks can be used to implement undo and redo functionality in applications, such as text editors and image editors. By maintaining a stack of previous states, the application can easily undo and redo actions, by popping and pushing states from the stack.
3. Syntax Checking: Stacks can be used in parsing and syntax checking of programming languages. For example, in a compiler or interpreter, a stack can be used to keep track of the current state of the program being parsed, such as keeping track of matching brackets or keeping track of function calls. This allows for efficient and accurate checking of the syntax of the program, and aids in error handling.

## Termwork 2 - infix to postfix
### Algorithm
1. Create an empty stack.
2. Initialize an empty string (result) to store the postfix expression.
3. Iterate through each character of the prefix expression, starting from the rightmost character.
4. If the current character is an operand, append it to the result string.
5. If the current character is an operator, pop the top two elements from the stack and append them to the result string, separated by the current operator. Then, push the current operator onto the stack.
6. Repeat steps 3-5 for all characters of the prefix expression.
7. Once all characters have been processed, pop any remaining operators from the stack and append them to the result string.
8. Reverse the result string and return it as the postfix expression.
### IO
```bash
 * ➜  programs git:(ds) ✗ gcc tw2.c && ./a.out
 * Output 1
 * Enter the exp: 4-6+7*7
 * 46-77*
 * 
 * Output 2
 * Enter the exp: 7-4+3^5
 * 74-35^
 * 
 * Output 3
 * Enter the exp: 3+5+4
 * 35+4+
```
### Applications
Same as termwork 1

## Termwork 3 - queue
### Algorithm
1. Create an empty queue.
2. Define a function for enqueuing an element into the queue.
 - Within this function:
 - Check if the queue is full. If it is, display an error message and return.
 - If the queue is not full, add the element to the rear of the queue.
3. Define a function for dequeuing an element from the queue.
 - Within this function:
 - Check if the queue is empty. If it is, display an error message and return.
 - If the queue is not empty, remove the element from the front of the queue.
4. Define a function for displaying the elements of the queue.
 - Within this function:
 - Check if the queue is empty. If it is, display an error message and return.
 - If the queue is not empty, iterate through the queue and print each element.
### IO
```bash
➜  programs git:(main) ✗ gcc tw3-new.c&&./a.out                                                                                     
1. Enqueue
2. Dequeue
3. Display
4. Exit   
Enter choice: 1
Enter the element to be enqueued: 4
4 enqueued to queue
4 enqued      
1. Enqueue
2. Dequeue
3. Display
4. Exit
Enter choice: 1
Enter the element to be enqueued: 5                                                                                                 
5 enqueued to queue
5 enqued  
1. Enqueue
2. Dequeue
3. Display     
4. Exit                         
Enter choice: 1
Enter the element to be enqueued: 8
8 enqueued to queue
8 enqued  
1. Enqueue
2. Dequeue
3. Display     
4. Exit       
Enter choice: 3
Queue elements: 4 5 8
          
1. Enqueue
2. Dequeue     
3. Display                                                                                                                          
4. Exit
Enter choice: 2
4 dequeued from queue
1. Enqueue
2. Dequeue
3. Display
4. Exit
Enter choice: 2
5 dequeued from queue
1. Enqueue
2. Dequeue
3. Display
4. Exit
Enter choice: 2
8 dequeued from queue
1. Enqueue
2. Dequeue
3. Display
4. Exit
Enter choice: 3
Queue is empty
1. Enqueue
2. Dequeue
3. Display
4. Exit
Enter choice: 4
➜  programs git:(main) ✗
```
### Applications
1. Job Scheduling: Queues can be used to implement job scheduling in a system. For example, in a multi-tasking operating system, jobs are placed in a queue, and are executed in the order they were received. This way, the system can efficiently manage and execute multiple tasks at the same time.
2. Communication between threads: Queues can be used to implement communication between threads in a program. For example, one thread can add messages to a queue, and another thread can retrieve and process the messages from the queue. This way, the threads can efficiently share data and communicate with each other without the need for direct access to shared memory.
3. BFS traversal: Queues are used in breadth first search (BFS) algorithm to traverse a tree or graph data structure. The algorithm starts from a root node and visits all the adjacent nodes at the present depth before moving on to the next level. The queue stores the nodes to be visited next, it is used to keep track of the nodes that are waiting to be visited and the algorithm follows the FIFO rule of queue to traverse the tree level by level.

## Termwork 4 - doubly linked list
### Algorithm
1. Create an empty doubly linked list with a head and tail pointer.
2. Define a function for adding an element to the doubly linked list.
 - Within this function:
 - Create a new node with the element and its next and previous pointers set to null.
 - Check if the doubly linked list is empty, if so, set the new node as the head and tail.
 - If the doubly linked list is not empty, append the new node to the tail of the list by updating the next pointer of the current tail to point to the new node and the previous pointer of the new node to point to the current tail.
3. Define a function for displaying the elements of the doubly linked list.
 - Within this function:
 - Check if the doubly linked list is empty, if so, display an error message and return.
 - If the doubly linked list is not empty, starting from the head of the list, iterate through the list by following the next pointers and print each element.

### IO
```bash
 * ➜  programs git:(ds) ✗ gcc tw4.c && ./a.out
 * 
 * 1: Add item    2: Display   3: exit
 * Enter your option: 1
 * 
 * Enter item to add to list: 1
 * 
 * 1: Add item    2: Display   3: exit
 * Enter your option: 5
 * 
 * 1: Add item    2: Display   3: exit
 * Enter your option: 1
 * 
 * Enter item to add to list: 6
 * 
 * 1: Add item    2: Display   3: exit
 * Enter your option: 2
 * 
 * The list items are: 1    6    
 * 1: Add item    2: Display   3: exit
 * Enter your option: 1
 * 
 * Enter item to add to list: 9
 * 
 * 1: Add item    2: Display   3: exit
 * Enter your option: 1
 * 
 * Enter item to add to list: 4
 * 
 * 1: Add item    2: Display   3: exit
 * Enter your option: 2
 * 
 * The list items are: 1    4    6    9    
 * 1: Add item    2: Display   3: exit
 * Enter your option: 3
```
### Applications
1. Dynamic Memory Allocation: Linked lists can be used to implement dynamic memory allocation in a program. Because linked lists do not have a fixed size, they can easily grow and shrink as needed, making them well suited for managing memory in a program.
2. Dynamic Data Structures: Linked lists can be used to implement dynamic data structures, such as lists, stacks, and queues, that can grow and shrink as needed. Linked lists are particularly useful in situations where the size of the data structure is not known in advance.
3. Data Management: Linked lists can be used to efficiently manage and organize large amounts of data, such as in databases or file systems. For example, a linked list can be used to implement a hash table, which is a data structure used to efficiently store and retrieve data based on a key. Linked lists also can be used to efficiently implement a cache memory in the computer system.

## Termwork 5 - trees
### Algorithm
1. Create a function for preorder traversal.
 - Within this function:
 - Print the root node.
 - Perform a preorder traversal on the left subtree.
 - Perform a preorder traversal on the right subtree.
2. Create a function for inorder traversal.
 - Within this function:
 - Perform an inorder traversal on the left subtree.
 - Print the root node.
 - Perform an inorder traversal on the right subtree.
3. Create a function for postorder traversal.
 - Within this function:
 - Perform a postorder traversal on the left subtree.
 - Perform a postorder traversal on the right subtree.
 - Print the root node.

### IO
```bash
 * ➜  programs git:(ds) ✗ gcc tw5.c && ./a.out
 * Enter a node 4
 * Enter a node 5
 * Enter a node 7
 * Enter a node 4
 * Enter a node 2
 * Enter a node 9
 * Enter a node 4
 * Enter a node 8
 * Inorder traversal: 2 -> 4 -> 4 -> 4 -> 5 -> 7 -> 8 -> 9 -> 
 * After deleting 10
 * Inorder traversal: 2 -> 4 -> 4 -> 4 -> 5 -> 7 -> 8 -> 9 ->
```

### Applications
1. Data Searching and Retrieval: Trees are commonly used in data searching and retrieval algorithms, such as binary search trees, AVL trees, and B-trees. These data structures allow for efficient searching, insertion, and deletion of data, making them well suited for applications such as databases and file systems.
2. Decision Making: Trees are used in decision-making algorithms, such as decision trees and decision forests. These algorithms are used in a wide range of applications, including machine learning, artificial intelligence, and game development.
3. Network Routing: Trees are used in network routing algorithms, such as spanning trees, which are used to find the shortest path between nodes in a network. These algorithms are used in a wide range of applications, such as telecommunications networks and transportation networks, to optimize the flow of information and resources.
## Termwork 6 - binary search
### Algorithm
1. Create a function for binary search.
 - Within this function:
 - Take an array, the number of elements in the array and the element to be searched as inputs.
 - Initialize the start index to 0 and the end index to n-1, where n is the number of elements in the array.
 - while (start <= end)
    - calculate the middle index as (start + end) / 2
    - if (arr[middle] == element)
      - return the index of the element
    - else if (arr[middle] < element)
      - set the start index to middle + 1
    - else (arr[middle] > element)
      - set the end index to middle - 1
    - if element not found in the array, return -1.
### IO
```bash
➜  programs git:(main) ✗ gcc tw6.c&&./a.out                                                                                         

 enter n value5

 Array Elements are ...0 1 2 3 4 
 Enter Key element2
Time taken = 0.481646Key element found%                                                                                             ➜  programs git:(main) ✗ gcc tw6.c&&./a.out                                                                                         

 enter n value15

 Array Elements are ...0 1 2 3 4 5 6 7 8 9 10 11 12 13 14 
 Enter Key element3
Time taken = 0.818928
Key element found%                                                                                                                  ➜  programs git:(main) ✗ gcc tw6.c&&./a.out                                                                                         

 enter n value8

 Array Elements are ...0 1 2 3 4 5 6 7 
 Enter Key element4
Time taken = 1.276266
Key element found%                                                                                                                  ➜  programs git:(main) ✗ 
```
### Applications
1. Searching large datasets: Binary search is an efficient algorithm for searching large datasets, such as arrays and sorted lists. It works by repeatedly dividing the search interval in half, until the desired element is found. This allows the algorithm to search a large dataset in a relatively short amount of time.
2. Sorted data look up: Binary search can be used to quickly find the position of an element in a sorted list. This is useful in many applications such as searching through a large list of contacts, searching a large dictionary and searching a large array of elements.
3. Optimizing time complexity: Binary search can also be used to optimize the time complexity of certain algorithms. For example, if a program needs to check if an element is present in a large dataset, it can use binary search to quickly find the element, rather than iterating through the entire dataset. This can greatly reduce the amount of time required to complete the task.
## Termwork 7 - quick sort
### Algorithm
1. Create a function for quick sort.
 - Within this function:
 - Take an array and the number of elements in the array as inputs.
 - If the number of elements in the array is less than 2, return the array.
 - Choose a pivot element from the array.
 - Create two empty arrays, one for elements less than the pivot and one for elements greater than the pivot.
 - Iterate through the array and place each element in the appropriate array.
 - Recursively call the quick sort function on the array of elements less than the pivot and the array of elements greater than the pivot.Concatenate the sorted array of elements less than the pivot, the pivot element, and the sorted array of elements greater than the pivot.
### IO
```bash
➜  programs git:(main) ✗ gcc tw7.c&&./a.out                                                                                          
Unsorted array:45 85 86 86 19 84 100 66 33 59 80 21 37 47 55 75 48 51 36 31 31 65 16 45 30 51 84 10 12 26 44 56 62 82 93 32 65 44 97 97 54 77 18 90 75 24 65 75 74 52 5 4 68 21 100 49 23 84 58 86 61 54 93 74 35 37 6 51 80 2 47 86 30 16 75 57 39 91 31 12 42 35 15 61 7 67 10 29 2 19 66 14 72 58 87 58 94 44 8 26 
Sorted array: 2 2 4 5 6 7 8 10 10 12 12 14 15 16 16 18 19 19 21 21 23 24 26 26 29 30 30 31 31 31 32 33 35 35 36 37 37 39 42 44 44 44 45 45 47 47 48 49 51 51 51 52 54 54 55 56 57 58 58 58 59 61 61 62 65 65 65 66 66 67 68 72 74 74 75 75 75 75 77 80 80 82 84 84 84 85 86 86 86 86 87 90 91 93 93 94 97 97 100 100 
Time taken by program is: 0.000008
➜  programs git:(main) ✗ gcc tw7.c&&./a.out                                                                                         
Unsorted array:53 8 7 63 84 9 7 64 59 55 83 53 48 37 22 78 32 82 43 88 67 28 98 100 85 67 69 48 95 49 13 47 56 19 61 91 79 68 6 37 22 40 42 21 29 15 50 60 96 93 47 15 72 44 14 8 62 35 55 56 83 67 54 90 37 15 32 68 34 38 56 7 29 97 27 57 12 76 68 59 20 14 73 91 9 87 50 71 73 5 78 55 23 32 44 12 98 75 79 31 
Sorted array: 5 6 7 7 7 8 8 9 9 12 12 13 14 14 15 15 15 19 20 21 22 22 23 27 28 29 29 31 32 32 32 34 35 37 37 37 38 40 42 43 44 44 47 47 48 48 49 50 50 53 53 54 55 55 55 56 56 56 57 59 59 60 61 62 63 64 67 67 67 68 68 68 69 71 72 73 73 75 76 78 78 79 79 82 83 83 84 85 87 88 90 91 91 93 95 96 97 98 98 100 
Time taken by program is: 0.000013
```
### Applications
1. Sorting large datasets: Quick sort is a highly efficient sorting algorithm that can quickly sort large datasets. It works by partitioning the dataset into smaller sub-arrays and then recursively sorting each sub-array. This allows the algorithm to sort a large dataset in a relatively short amount of time.
2. Optimizing time complexity: Quick sort can be used to optimize the time complexity of certain algorithms. For example, if a program needs to sort a large dataset, it can use quick sort to quickly sort the dataset, rather than using other sorting algorithms that may take longer.
3. Searching and Retrieval of data: Quick sort can be used to sort a large dataset, which can be then used for searching and retrieval of data in efficient way. Once the data is sorted, the search algorithms like binary search can be applied to search for specific data in the dataset.

## Termwork 8 - greedy prims algoritm

### Algorithm
1. Initialize the minimum spanning tree with an arbitrary starting vertex.
2. Maintain a priority queue of edges that connect the vertices in the minimum spanning tree with vertices not yet in the tree.
3. Select the edge with the smallest weight from the priority queue and add the corresponding vertex to the minimum spanning tree.
4. Repeat step 3 until all vertices are in the minimum spanning tree.
5. At this point, the minimum spanning tree is complete, and the edges that connect the vertices in the tree correspond to the shortest paths between the vertices.

### IO
```bash
Output 1
Enter the number of nodes:5

Enter the adjacency matrix:
0 2 0 6 0
2 0 3 8 5
0 3 0 0 7
6 8 0 0 9
0 5 7 9 0


 Edge 1:(1 2) cost:2
 Edge 2:(2 3) cost:3
 Edge 3:(2 5) cost:5
 Edge 4:(1 4) cost:6
 Minimun cost=16

Output 2

Enter the number of nodes:4

Enter the adjacency matrix:
1 2 0 5
2 0 0 7
0 5 8 4
9 7 4 0


 Edge 1:(1 2) cost:2
 Edge 2:(1 4) cost:5
 Edge 3:(4 3) cost:4
 Minimun cost=11

Output 3
Enter the number of nodes:6 

Enter the adjacency matrix:
0 0 0 0 8 9
6 5 8 0 0 3
2 0 8 0 4 3
0 6 9 0 4 0
1 6 0 3 0 4
0 0 0 6 0 9


 Edge 1:(1 5) cost:8
 Edge 2:(5 4) cost:3
 Edge 3:(5 6) cost:4
 Edge 4:(4 2) cost:6
 Edge 5:(2 3) cost:8
 Minimun cost=29
```

### Applications
1. Network Design: Prim's algorithm is commonly used in network design to find the minimum cost tree that connects all nodes in a network. The algorithm can be used to optimize the design of communication networks, computer networks, and transportation networks.
2. Image Segmentation: Prim's algorithm can be used in image processing to segment images into separate regions. The algorithm can be used to find the minimum spanning tree of the graph that represents the image, and then used to segment the image into separate regions based on the edges in the minimum spanning tree.
3. Cluster Analysis: Prim's algorithm can be used in data analysis to cluster data into groups based on their similarity. The algorithm can be used to find the minimum spanning tree of a graph that represents the data, and then used to cluster the data into groups based on the edges in the minimum spanning tree.

## Termwork 9 - Dynamic programming floyds algorithm
### Algorithm
1. Initialize the distance matrix: Create an n x n matrix, where n is the number of vertices in the graph, and initialize all elements in the matrix to the weight of the edge between the corresponding vertices. If there is no edge between two vertices, the weight should be set to infinity.
2. Iterate over intermediate vertices: For each intermediate vertex k in the range 1 to n, repeat the following steps:
  - For each pair of vertices i and j in the range 1 to n, check if the distance between i and j can be improved by using vertex k as an intermediate vertex.
  - If the distance can be improved, update the distance matrix.
3. Return the distance matrix: The final distance matrix contains the shortest distances between all pairs of vertices in the graph.

### IO
```bash
Floyds Algorithm 
Enter number of nodes :2

 Enter the edge weights :3 4 
5 6
matrix D[1]
3       4
5       6
matrix D[2]
3       4
5       6
➜  programs git:(main) ✗ gcc tw9.c&&./a.out
Floyds Algorithm 
Enter number of nodes :3 

 Enter the edge weights :5 7 0
8 7 0
0 0 1
matrix D[1]
5       7       0
8       7       0
0       0       0
matrix D[2]
5       7       0
8       7       0
0       0       0
matrix D[3]
0       0       0
0       0       0
0       0       0
➜  programs git:(main) ✗ gcc tw9.c&&./a.out
Floyds Algorithm 
Enter number of nodes :4

 Enter the edge weights
7 0 0 0
0 8 0 0
0 0 6 0
0 0 0 1
matrix D[1]
7       0       0       0
0       0       0       0
0       0       0       0
0       0       0       0
matrix D[2]
0       0       0       0
0       0       0       0
0       0       0       0
0       0       0       0
matrix D[3]
0       0       0       0
0       0       0       0
0       0       0       0
0       0       0       0
matrix D[4]
0       0       0       0
0       0       0       0
0       0       0       0
0       0       0       0
```
### Applications
1. Shortest Paths in Weighted Graphs: One of the main applications of Floyd's algorithm is to find the shortest path between all pairs of vertices in a weighted graph. This is useful in a variety of applications, such as route planning, network design, and more.
2. Transitive Closure of a Graph: Another application of Floyd's algorithm is to find the transitive closure of a graph, which is the set of all pairs of vertices that are reachable from each other. This can be useful in various applications, such as network analysis, resource allocation, and more.
3. Detecting Negative Cycles: Floyd's algorithm can also be used to detect negative cycles in a graph. A negative cycle is a cycle of edges in a graph where the sum of the edge weights is negative. This can be useful in various applications, such as financial analysis, resource allocation, and more.

## Termwork 10 - Backtracking floyds algorithm
### Algorithm
1. Initialize the chessboard: Create an n x n chessboard and initialize all cells to be empty.
2. Place the first queen: Place the first queen in the first row of the first column.
3. Place subsequent queens: For each subsequent queen, repeat the following steps:
  - For each row in the current column, check if the row is a safe place to place the queen.
  - If the row is a safe place, place the queen in that row and move to the next column.
  - If no safe row is found in the current column, backtrack to the previous column and try a different row.
4. Check for solutions: If all n queens have been placed, the solution is considered to be found. If not, repeat from step 3.
5. Return the solution: Return the solution as an array of row numbers, one for each queen, indicating the row in which the queen is placed.
### IO
```bash
Output 1
Enter the Number of queens
3

Total Number of Solutions=0%                                                                                                           
Output 2
Enter the Number of queens
4


Solution #1 

*       Q       *       *
*       *       *       Q
Q       *       *       *
*       *       Q       *


Solution #2 

*       *       Q       *
Q       *       *       *
*       *       *       Q
*       Q       *       *

Total Number of Solutions=2%                                                                                                           
Output 3
Enter the Number of queens
5


Solution #1 

Q       *       *       *       *
*       *       Q       *       *
*       *       *       *       Q
*       Q       *       *       *
*       *       *       Q       *


Solution #2 

Q       *       *       *       *
*       *       *       Q       *
*       Q       *       *       *
*       *       *       *       Q
*       *       Q       *       *


Solution #3 

*       Q       *       *       *
*       *       *       Q       *
Q       *       *       *       *
*       *       Q       *       *
*       *       *       *       Q


Solution #4 

*       Q       *       *       *
*       *       *       *       Q
*       *       Q       *       *
Q       *       *       *       *
*       *       *       Q       *


Solution #5 

*       *       Q       *       *
Q       *       *       *       *
*       *       *       Q       *
*       Q       *       *       *
*       *       *       *       Q


Solution #6 

*       *       Q       *       *
*       *       *       *       Q
*       Q       *       *       *
*       *       *       Q       *
Q       *       *       *       *


Solution #7 

*       *       *       Q       *
Q       *       *       *       *
*       *       Q       *       *
*       *       *       *       Q
*       Q       *       *       *


Solution #8 

*       *       *       Q       *
*       Q       *       *       *
*       *       *       *       Q
*       *       Q       *       *
Q       *       *       *       *


Solution #9 

*       *       *       *       Q
*       Q       *       *       *
*       *       *       Q       *
Q       *       *       *       *
*       *       Q       *       *


Solution #10 

*       *       *       *       Q
*       *       Q       *       *
Q       *       *       *       *
*       *       *       Q       *
*       Q       *       *       *

Total Number of Solutions=10%   
```
### Applications
1. Combinatorial Search: Backtracking is commonly used in combinatorial search problems where the goal is to find all possible combinations of elements that satisfy certain constraints. For example, backtracking can be used to find all possible solutions to the N-Queens problem, where the goal is to place N queens on an NxN chessboard such that no two queens attack each other.
2. Solving Constraint Satisfaction Problems: Backtracking can also be used to solve constraint satisfaction problems, where the goal is to find a solution that satisfies a set of constraints. For example, backtracking can be used to find a solution to a crossword puzzle, where the goal is to fill in the puzzle with words such that each word fits into the puzzle and does not overlap with any other words.
3. Generating Permutations and Combinations: Backtracking can also be used to generate all possible permutations and combinations of a given set of elements. For example, backtracking can be used to generate all possible permutations of a given string, or to generate all possible combinations of a given set of items.