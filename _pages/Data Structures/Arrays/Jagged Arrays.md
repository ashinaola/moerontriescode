---
title: "Jagged Arrays: Taking Them to the Next Level"
date: "2025-05-19"
bookmark: true
thumbnail: "/assets/img/thumbnail/jaggedarray.png"
---

There are several types of arrays which can be serve different purposes.  While there are more types, the main focus will be on jagged arrays.  The characteristic of this data structure can be summarized as an 'array of arrays'.  The jagged array is made of arrays of different sizes or lengths.  The jagged arrays may have some differences compared with the introduced static array.  For example, the composition of arrays adds another dimension to the structure relative to the static array.

# Operations
As previously mentioned, jagged arrays set themselves apart from 2-D arrays due to the fact that it is comprised of arrays of different lengths.  This would alter how inserts, deletes, searches, and traversals are implemented.  It can also alter the runtime of the operations, due to the additional dimension which adds another layer of traversal.  By creating a code segment, it is easier to demonstrate how the operations work and are implemented.  The code to initiate the jagged array will be as follows:
```

#include <iostream>
#include <vector>
#include <string>
using namespace std;

class JaggedArray {
public:
    vector<string> outerArray;

    JaggedArray() {
        // Optional: initialize or log something
    }
}
```

The array will take in a file which has several addresses and store them in the structure.  By creating this structure, it is possible to organize text file contents into an array and make it easier to merge several text files together, for example.  While the original idea behind the jagged array is to have an array of arrays which are static, the outer array of the jagged array will be a vector instead.  Vectors are essentially dynamic arrays which can grow in order to accomodate more data than initally reserved.  This property will allow us to take in more lines from text files, which will allow us to easily concatenate two text files of addresses into one single jagged array.

## Insert
After creating the jagged array structure, the first operation to work on would be the insert operation.  The steps of the insert() would go as follows:
> 1. Take in the string array which represents a row in the text file.
> 2. Add the string array to the vector.

Added elements in this example would be arrays of strings which were created by reading in a file line by line.  Again, what would make this array jagged is the fact that each string will have a different amount of indices.  If the arrays which were added all shared the same length, it would be a 2-D array instead of an jagged array.  The following is a code snippet, representing the function which performs inserts for the jagged array:
```

void insertElement(string[addrSize] addr) {
    outerArray.push_back(addr);
}
```

## Delete
After adding elements to the jagged array, there should be a way for the operation to be undone.  This will allow for elements to be deleted after being added.  For example, if the wrong or corrupted array is entered, the data structure can undo the operation by executing a delete function.  There can be several ways for a jagged array to execute a delete.  One way is for the function parameters to provide the element index, so that the proper indices are freed:
```
void deleteElement(int index){
    // delete action goes here
}
```
Another way is for the string or string array to be provided and then search for the matching entrance.  While this can be ideal when the element indices are unknown, the first methodology would be more efficient due to the worst case search being O($$ n^2 $$).  Deleting an element from the outer vector will run at constant time, which is a better implentation of the delete operation, despite the difference in signature:
```
void deleteElement(int index) {
    if (!outerVector.empty()) {
        if (index >= 0 && index < outerVector.size()) {
            outerVector.erase(outerVector.begin() + index);
        } else {
            std::cout << "Invalid index: Out of bounds." << std::endl;
        }
    } else {
        std::cout << "Empty vector: Please insert elements." << std::endl;
    }
}
```
The code segment will check the length to make sure that the vector has elements to remove before proceeding to delete the element at the provided index.  The index can be provided either directly by the user or by another function, search() which will return the index of the matching function.  The output from the search can be used as the function parameter of the deleteElement() funtion.

## Traverse
The traversal operation for the jagged array is different from the static array, or dynamic array (vector) due to its property of having multiple dimensions.  However, unlike the 2-D array, the jagged array is not perfectly 2-D.  Technically, traversing the jagged array will take $$ \lt $$ O($$ n^2 $$).  For practical purposes, it is easier for the traversal to be counted as running in the worst case of O($$ n^2 $$) runtime.

To execute the traversal of the jagged array, it must start at the initial index and traverse down each element in the vector.  Since each element is an array, the array is traversed before moving to the next element in the vector.  This would call for a nested loop as shown:
```
void traversal() {
    for (int i = 0; i < outerArray.size(); ++i) {
        std::cout << "Row " << i << ": ";
        for (int j = 0; j < outerArray[i].size(); ++j) {
            std::cout << outerArray[i][j] << " ";
        }
        std::cout << std::endl;
    }
}
```

## Linear Search
As mentioned in the introductory section, searches in jagged arrays are similar in the sense that the operation aims to find the matching element and return the index.  There are multiple ways searches can be conducted. Depending on the size of the jagged array being searched, the appropriate search method with the correct runtime should be used as the search function's algorithm.  Since the input size will not be too large, a simple search algorithm which takes o($$ n^2 $$) runtime will be acceptable, however it will not be the best search if the jagged array were to grow upwards in size.  This would exponentially increase the amount of comparisons which would slow down the execution time of the program.  It would be appropriate to adjust the search to an algorithm which runs at a faster runtime.

The code segment of the search will start at the first element or the array and assess whether the strings match, before traversing down the inner-array until an unmatching element is met.  If a string doesn't match, then the algorithm should move to the next element and traverse down.  If the end of the array is met, the loop can be stopped and the index of the matching array returned by the function.  Here is a snippet of the function:
```
int search(string addr[]) {
    for (int i = 0; i < outerArray.size(); ++i) {
        if (outerArray[i] == addr) {
            return i; // Found a match at index i
        }
    }
    return -1; // Not found
}
```

# Jagged Arrays: Uses and Examples
In this example, the goal is to utilize the jagged array to take two different text files of addresses and merge them into a singular storage location, which will be the jagged array.  The jagged array can offer a singular location for content distributed across different text files, a singular location to manage the addresses.  The challenge is to create a tokenizer, so that the read-in lines can be plugged into the data structures and then read each line into the jagged array.  By compiling and executing the program, two text files can be merged into the jagged array and display the contents from one single location.


