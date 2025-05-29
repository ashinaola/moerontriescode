---
title: "Introduction to Arrays"
date: "2025-05-19"
bookmark: true
thumbnail: "/assets/img/thumbnail/arraypic.gif"
---

In many situations, the ability to take multiple values and assign them to one variable is can be desired.  For example, if you want to keep track of the highest scores of a game and display them, it would help to have a running list of scores to compare against.  Arrays are a way to store values to be retrieved later.  Due to its versatile nature, it has been used in many different solutions and algorithms.

An array is usually the first data structure that is introduced due to its intuitive nature.  This is because an array is defined as an contiguous block of memory.  As such, arrays usually are defined and limited to a single type as well as the length.  There is a different form of array, considered dynamic arrays, which can adjust its length as more elements are added to the array.  However, since the memory block is defined upon initiation of the array, the array length itself can not be extended.

# Arrays: Operations
Arrays are normally zero-indexed (with the exception of some languages such as Lua) which means that the array indexes start at 0 and increases as the it is being traversed.  The usefulness of the indexes allow for elements to be stored and retrieved easily, which makes it a useful basic structure to utilize when storing data.  Arrays normally offer five operations; insertion, deletion, traversal, searching, and sorting, which make them useful in applying them to solve different problems.  The indexed property of the array allows for the elements of the data structure to be organized and retrieved in constant time, which would allow for programs to store larger amounts of data.

To demonstrate the five operations, an array which holds integers will be initialized.  Even though the operations are being applied to integers, the same actions can be applied to strings, characters, floats/doubles, booleans, all the way to objects and structures.  Arrays can even hold other arrays (Refer to 2-D Arrays [here](./2-D%20Arrays.md)). 
To start, an array should be declared as follows:
```
// declare an array which holds five integers
int[5] demoArray;
```
> Please note that the code fragments are not complete classes and are not ready to compile

## Insertion
The first operation to perform on the array after declaring would be to assign values to the array.  The language that we are utilizing is C++, which means that the types of elements which can be stored in the array is defined at the declaration of the array.  There are other languages which are more flexible with types, such as Javascript and Python, however those structures are a bit different from the traditional array.  When insertion is performed on an array, it executes in constant time.
```
// insert the first element into the array
demoArray[0] = 1;
demoArray[1] = 2;
```
The code above takes the integers 1 and 2, then adds them to the index of the array.  This is added in constant time, as the insertion can simply assign the integers by index. Insertions are important since they allow for the data to be stored for later retrievals.  Insertions only can work within the range which was defined.  If an insertion was to be executed to an index that is outside of the defined range, it would result in an Out of Bounds error:
```
// returns an error due to the index being out of bounds
demoArray[5] = 6;
```

## Deletion
As an static structure, arrays do not have the capability to change its size.  This makes direct deletion of elements not possible, however deletion can be mimicked.  The steps to deleting an element from the array goes as follows:

>1. Find the desired element to delete from the array: 
> either through index or matching element
>2. Shift the remaining elements one space to the left (fill in the gap)

Due to the 2nd step, the deletion of an element from an static array gives the worst case runtime of O($$ n $$).  This is because the worst case assumes that the matching element is not found, thus not deleted.  This demonstrates a different runtime from the insertion operation of an static array, which has to be factored when attempting to utilize an static array for an solution.  While there is an advantage with inserting and retrieving elements from the array, deletes are a costlier operation when using the static array.  This trade off should be considered when implementing solutions to various problems.

So to demonstrate an deletion, the previously initialized demoArray would start with two elements after the insertions and end with one element.  
> demoArray -> [1,2]
> demoArray -> [0,2] , the 1 was deleted
> demoArray -> [2,]  , the 2 was shifted one index to the left

Here is the deletion being applied as a function:
```
void deleteElement(int demoArray[], int& size, int element) {
    int elmIndex = -1;

    // Find the index of the element to delete
    for (int i = 0; i < size; i++) {
        if (demoArray[i] == element) {
            elmIndex = i;
            break;
        }
    }

    if (elmIndex == -1) {
        cout << "Element not found" << endl;
        return;
    }

    // Shift elements to the left
    for (int i = elmIndex; i < size - 1; i++) {
        demoArray[i] = demoArray[i + 1];
    }

    // Decrease the size of the array
    size--;
}
```

## Traversal
Traversal is a frequently used operation not only for arrays, but for other data structures as well.  Traversal is where each index or element stored on the structure is visited.  This gives traversal of the array a worst-case runtime of O($$ n $$).  Traversal is central to linear search, where the array is traversed to find a specific element in the array.  It is also utilized to print out array elements, which can be useful for debugging programs to find misallocated or misassigned variables.

Traversal starts on the first index of the array and iterates through the array until it has visited every index on the array.  For some languages, the array's index will start at 1 (such as Lua), while others start at 0 (such as Javascript, Java, C++, and Python).  The reason is because the loop will either end at the nth index (if it starts at 1) or (n-1)th index.  The following code can be used to execute a traversal:
```
void traversal(int demoArray[], int& arraySize) {
    // start at the beginning of the array
    int itr = 0;

    // loop through the array and print the element until the end is reached
    while(itr < arraySize) {
        cout << "element: " << demoArray[itr] << endl;
        itr++;
    }
}
```

## Searching
Another operation which are common in arrays is searching, where the provided element is provided and the array is traversed until the desired element is found.  This is a particular style of searching called linear search which has a runtime of O($$ n $$).  There are other forms of search which has faster runtimes which will be explored in other posts, such as binary search, however the focus will be in implementation of linear search.

> Start at the first element
> Check if element is matching:
> If true: return true and break
> Return false 

The linear search is one of the introductory searches which students get familiar with and its intuitive approach to finding elements make it a general useful tool for the presented problem of finding the element in a static array.  This code segment is an implementation of a typical linear search, using the demoArray example:
```
int linearSearch(int demoArray[], int arraySize, int element) {
    for(int i = 0; i < arraySize; i++) {
        if (demoArray[i] == element) {
            return i;
        }
    }
    return -1;
}
```

## Sorting
There are several sorting algorithms which are utilized to sort array contents, however we will not explore them in depth.  Depending on the algorithm, the runtime can range from polynomial to factorial.  The algorithm that we will look at has a quadratic, or O($$ n^2 $$), time.  There are several sorting algorithms that can be discussed at this runtime, such as selection and insertion sort, however we will focus on bubble sort.

The goal of all sorting algorithms, including bubble sort, is to take a static array of elements and place the elements in ascending or descending order.  While its runtime is O($$ n^2 $$), it does not require any additional memory space and performs relatively well on nearly-sorted arrays.  The main problem with bubble sort is its inefficiency with larger datasets, which may cause it to be less favorable when considering real life applications.  Bubble sort is still a useful algorithm to introduce the sorting problem and work through it with an intuitive solution.

The steps of bubble sort to create an sorted array in ascending order is as follows:

> 1. Start at the first index of array ($$ reference_1 $$)
> 2. Start $$ reference_2 $$, traverse down the array
> 3. At each step compare $$ reference_2 $$ to $$ reference_1 $$
> 4. Swap values if $$ reference_1 > reference_2 $$
> 5. Continue unitl $$ reference_1 $$ reaches the end

The reason for the worst case runtime of O($$ n^2 $$) is because of the amount of comparisons which are executed as the first reference is going down the list.  For each index, the algorithm traverses down the list and executes comparisons against each element giving $$ n * (n-1) $$ or $$ n^2 $$ runtime.  The following is a code snippet of bubble sort:
```
void bubbleSort(int demoArray[], int arraySize) {
    for (int i = 0; i < arraySize - 1; i++) {
        for (int j = 0; j < arraySize - i - 1; j++) {
            if (demoArray[j] > demoArray[j + 1]) {
                // Swap
                int temp = demoArray[j];
                demoArray[j] = demoArray[j + 1];
                demoArray[j + 1] = temp;
            }
        }
    }
}

```

# Arrays: Examples and uses
Arrays are in wide use in programming and there are many examples where arrays are appropriate to be applied.  For example, it offers a useful data storage mechanism which allows for easy retrieval.  This would make it an ideal solution for any problem which calls for easy retrieval where the index of the desired element is known.  This will take advantage of the array's constant time retrieval.  In video games, arrays usually store the leaderboard scores which are a common place feature.  By using the sorting operation, the top scores of the game can be ranked and retrieved.

There are other uses for arrays which include listing contacts on a cell phone, image storing on a computer, and many other similar uses.