+++
title = 'Basic data structures and algorithms in python'
date = 2025-02-25T09:13:40Z
tags = ["python", "data structures", "algorithms", "competitive programming"]
author = "Me"
showToc = true
TocOpen = false
draft = false
hidemeta = false
comments = false
description = "A short guide of data structures and algorithms in python"
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

# Basic data structures and algorithms in python

## Searching algorithms in python

### Linear search

```py
def linear_search(arr, target):
    for i in range(len(arr)):
        if arr[i] == target:
            return i  # Return the index if target is found
    return -1  # Return -1 if the target is not found

def main():
    arr = [3, 10, 23, 5, 2, 6]
    target = 5

    # Calling the linear_search function
    result = linear_search(arr, target)

    # Output the result
    if result != -1:
        print(f"Element {target} found at index {result}.")
    else:
        print(f"Element {target} not found in the list.")

# Calling main to run the program
if __name__ == "__main__":
    main()
```

Time Complexity
- Best Case: O(1) — This happens if the target element is found at the first index.
- Worst Case: O(n) — This happens if the target element is at the end of the list or not in the list at all.
- Average Case: O(n) — On average, the search will have to look through half of the list.

Space Complexity
- O(1) — The algorithm only uses a fixed amount of space regardless of the input size. There is no extra memory used other than a few variables (like i).

### Binary search

```py
def binary_search(arr, target):
    left, right = 0, len(arr) - 1
    
    while left <= right:
        mid = left + (right - left) // 2
        
        # Check if the target is present at mid
        if arr[mid] == target:
            return mid
        
        # If target is smaller than mid, search in the left half
        elif arr[mid] > target:
            right = mid - 1
        
        # If target is larger than mid, search in the right half
        else:
            left = mid + 1
    
    return -1  # Return -1 if the target is not found

def main():
    arr = [2, 5, 6, 10, 23]
    target = 10

    # Calling the binary_search function
    result = binary_search(arr, target)

    # Output the result
    if result != -1:
        print(f"Element {target} found at index {result}.")
    else:
        print(f"Element {target} not found in the list.")

# Calling main to run the program
if __name__ == "__main__":
    main()
```

Time Complexity
- Best Case: O(1) — The target is found at the middle index immediately.
- Worst Case: O(log n) — The search space is halved with each iteration.
- Average Case: O(log n) — As the search space keeps getting halved, the average time complexity is logarithmic.

Space Complexity
- O(1) — Only a few variables are used (like left, right, mid), so the space complexity is constant.

## Sorting algorithms

### Bubble sort
```py
def bubble_sort(arr):
    n = len(arr)
    
    # Traverse through all elements in the array
    for i in range(n):
        swapped = False
        
        # Last i elements are already sorted
        for j in range(0, n - i - 1):
            if arr[j] > arr[j + 1]:
                # Swap if the element found is greater than the next element
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
                swapped = True
        
        # If no two elements were swapped in the inner loop, the list is sorted
        if not swapped:
            break

def main():
    arr = [64, 34, 25, 12, 22, 11, 90]
    
    print("Unsorted array:")
    print(arr)

    # Calling the bubble_sort function
    bubble_sort(arr)

    print("\nSorted array:")
    print(arr)

# Calling main to run the program
if __name__ == "__main__":
    main()
```

Time Complexity:
- Best Case: O(n) — This happens if the array is already sorted, and the algorithm will only go through one pass.
- Worst Case: O(n²) — The algorithm must compare each element with every other element.
- Average Case: O(n²) — On average, the algorithm will make about n²/2 comparisons.

Space Complexity:
- O(1) — Only a constant amount of space is used for swapping elements.

### Insertion sort

```py
def insertion_sort(arr):
    for i in range(1, len(arr)):
        key = arr[i]
        j = i - 1
        
        # Move elements of arr[0..i-1] that are greater than key, one position ahead
        while j >= 0 and arr[j] > key:
            arr[j + 1] = arr[j]
            j -= 1
        
        arr[j + 1] = key

def main():
    arr = [12, 11, 13, 5, 6]
    
    print("Unsorted array:")
    print(arr)

    # Calling the insertion_sort function
    insertion_sort(arr)

    print("\nSorted array:")
    print(arr)

# Calling main to run the program
if __name__ == "__main__":
    main()
```

Time Complexity:
- Best Case: O(n) — This happens when the array is already sorted, and no shifts are needed.
- Worst Case: O(n²) — This happens when the array is sorted in reverse order, and every element must be compared and shifted.
- Average Case: O(n²) — Similar to the worst case, but on average, half of the comparisons will be needed for each element.

Space Complexity:
- O(1) — Only a constant amount of space is used for the key variable and a few comparisons.

### Quick sort

```py
def quick_sort(arr):
    if len(arr) <= 1:
        return arr
    
    # Choose a pivot (here, the last element is chosen as the pivot)
    pivot = arr[-1]
    left = [x for x in arr[:-1] if x <= pivot]  # Elements less than or equal to pivot
    right = [x for x in arr[:-1] if x > pivot]  # Elements greater than pivot
    
    # Recursively sort the left and right subarrays and combine them with pivot
    return quick_sort(left) + [pivot] + quick_sort(right)

def main():
    arr = [10, 7, 8, 9, 1, 5]
    
    print("Unsorted array:")
    print(arr)

    # Calling the quick_sort function
    sorted_arr = quick_sort(arr)

    print("\nSorted array:")
    print(sorted_arr)

# Calling main to run the program
if __name__ == "__main__":
    main()
```

Time Complexity:
- Best Case: O(n log n) — This happens when the pivot divides the array into roughly equal parts each time.
- Worst Case: O(n²) — This happens when the pivot is the smallest or largest element, causing the array to be split in a very unbalanced way.
- Average Case: O(n log n) — On average, the pivot divides the array fairly evenly.

Space Complexity:
- O(log n) — Due to the recursion stack, as the depth of recursion is proportional to log n for balanced partitions.