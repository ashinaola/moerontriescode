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
```

The array will take in a file which has several addresses and store them in the structure.  By creating this structure, it is possible to organize text file contents into an array and make it easier to merge several text files together, for example.  While the original idea behind the jagged array is to have an array of arrays which are static, the outer array of the jagged array will be a vector instead.  Vectors are essentially dynamic arrays which can grow in order to accomodate more data than initally reserved.  This property will allow us to take in more lines from text files, which will allow us to easily concatenate two text files of addresses into one single jagged array.

## Insert
After creating the jagged array structure, the first operation to work on would be the insert operation.  The steps of the insert() would go as follows:
    1. Take in the string array which represents a row in the text file.
    2. Add the string array to the vector.



## Delete

## Search

## Traverse

# Jagged Arrays: Uses and Examples
