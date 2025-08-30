---
title: "2-D Arrays: Introduction and Examples"
date: "2025-05-19"
bookmark: true
thumbnail: "/assets/img/thumbnail/2Darray.png"
---

In another post, the jagged array tool was introduced as a way to store and retrieve input which have varying length.  The structure was used to store a string of arrays in a vector.  As previously stated, a jagged array is an array which stores arrays of different lengths.  However, if an array were to store elements which were of equal lengths, the jagged array can be treated like an $$ m * n $$ matrix.  This structure is an 2-D array, which has been used to represent matrices and carry out matrix operations which are extremely useful across different domains.

# 2-D Array Tradeoffs
To begin, a 2-D array is thought of as an array of arrays.  Another way to think of 2-D arrays is an array whose elements are all arrays of equal length.  This creates a grid-like storage structure which can store elements in a table-like structure which offers the same constant-time retrieval as a single-dimensional array.  To initiate a 2-D array of integers in C++, an array can be initiated with each element being an array as so:
```
int exArray[4][2] = {
    {1, 2},
    {2, 3},
    {3, 4},
    {4, 5}
};
```
The code produces a 2 by 4 matrix:
$$ \begin{bmatrix}
1 & 2\\
2 & 3\\
3 & 4\\
4 & 5
\end{bmatrix} $$
This will allow for the integer element to be stored and worked with in the same way as one would work with a matrix in linear algebra.  However, while the array can be initiated in this way, modern C++ has offered the vector tool to help assist with memory management.  To use the vector methodology of initiating a 2-D array, a vector of int vectors are initiated as shown:
```
std::vector<std::vector<int>>
```
By using vector, memory management is handled and the storage can dynamically adjust to store more elements.

## Pros of 2-D Arrays
2-D arrays offer similar retrieval times as a singular array, which allows for the elements to be accessed in constant time.  By preserving the constant-time retrieval of single dimensional arrays, 2-D arrays can allow larger amounts of elements to be stored and retrieved by the program.

## Cons of 2-D Arrays
A major advantage of using the `std::vector` class to store elements compared to plain arrays, is that the `delete` keyword does not have to be invoked.  However, developers should be careful when using plain arrays for 2-D arrays.  When the 2-D array is used, the array has to be deallocated after initialization.  Failure to deallocate the memory will result in a memory leak due to C++ not having any garbage collection.  A reason for why a developer would want to utilize a plain array rather than use the `std::vector` class is to store a larger amount of elements and avoid the slight overhead which comes with utilizing the `std::vector` class.

When handling 2-D arrays, there should be care about how the program handles memory as well as accessing the array elements.  Traversal of the 2-D array is a great example, where it is recommended to traverse through columns using the inner portion of a nested loop and the row traversal being executed by the outer loop.  This would prevent the program from jumping to new memory locations to access elements within the array since the values are stored within contiguous blocks of memory.  Changing the iteration, by having the inner loop traverse the columns and the outer traverse the rows, will result in a slower execution time which would be problematic for larger inputs.
 
# 2-D Array: Use Cases
Because of its convenience and application accross different domains, 2-D arrays are used frequently to store multi-dimensional information.  Since 2-D arrays can be utilized as matrices, they can be seen in many areas which incorporate linear algebra as part of its solution.  Two areas where this is observed are in computer graphics and in deep learning solutions such as large language models (LLMs).

## Computer Graphics
In computer graphics, the 2-D array is used to store the pixels of the image in the form of decimal values.  The values can be used to map to the image, and linear transformations can be utilized to transform the image.  These solutions are useful in creating simulations and animations which drive discoveries in areas such as biology and physics.

## Large Language Models (LLMs)

# 2-D Array: Example - Linear Algebra Operations

## Dot Product

## Cross Product

## Matrix Multiplication