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
In computer graphics, the 2-D array is used to store the pixels of the image in the form of decimal values.  The values can be used to map to the image, and linear transformations can be utilized to transform the image.  These solutions are useful in creating simulations and animations which drive discoveries in areas such as biology and physics.  For instance, there is a useful library called OpenGL which enables the creation of 3-D objects and scences by configuring a camera and lights to add a more 'realistic' effect to the scene.  The OpenGL library is in the C++ environment and allows for one to build off of their knowledge of linear algebra to set up and manipulate 3-D objects.  This is the homepage to the OpenGL documentation page:
[OpenGL Homepage](https://www.opengl.org/) 

## Large Language Models (LLMs)
In recent years, there has been a major advancement in deep learning within the area of natural language processing.  Previously, chatbots were powered by Markov Chain models.  These were mathematical models which used a transition matrix to store different states and map the possibilities to them.  For example, imagine that a day's weather can be sunny, rainy, or cloudy.  The transition matrix would store the probalities that the sunny day would become cloudy or that the rainy day would become sunny, etc.  Each row of the matrix must have transition states which add to 1.  There also needs to be a way to tie together the states that are stored on the transition matrix which is where the Chapman-Kolmogrov equation comes in.  The Chapman-Kolmogrov equation states that the probability of moving from one state to another with steps in between would be equivalent to the product of all the transition values from the transition matrix.  The equation is defined as so:
$$ P^{m+n} (i + j) = \sum_{k} P^m (i,k) P^n (k,j) $$
With Markov Chains, it was possible to predict the next expected word which is being processed by a chatbot.  Or predict the overall context of the words sent by the user.  As seen here, before deep learning was utilized as a solution for chatbots, a 2-D array can be used as a data structure for the transition matrix.  However, one of the disadvantages which came with Markov chains were their unintuitive nature and limited scope which resulted in a limited chatbot.

During the 2010s, researchers began experimenting with recurring neural networks as a way to process text and speech input with the goal being to have a better prediction rate of the possible words.  There were various models such as GRUs (Gated Recurring Units) or LSTMs (Long Short Term Memory) which introduced new solutions which can be utilized in natural language processing.  These solutions work by generating the hidden states after processing the inputs and outputs of the model sequentially.  In practice, this can present several problems such as a vanishing gradient as well as a limited computability issue.  These can limit how well the models can handle more complex inputs and tasks.

To address the shortcomings of the GRUs and LSTMs, transformers were created to achieve a similar result but with a lower computing requirement.  This is because transformers posses the ability to process inputs and outputs in parallel instead of sequentially like GRUs.  This allows for transformers to be quickly trained relative to GRUs and LSTMs.  To implement training, matrices are used to store the encodings which will come in later during the training.  To implement programatically, it is not unusual to encounter vectors and 2-D arrays to store the encodings and positional encoding of the set.

# 2-D Array: Example - Linear Algebra Operations
After presenting some real world instances of 2-D arrays being part of bigger solutions, showing how some of the matrix operations are programmed can help visualize how powerful they can be as a store.  But it can also help show some of the bottlenecks that researchers may encounter while utilizing matrices to model complex real world problems.  Linear algebra is incorporated into many different disciplines including genomics, electromagnetism, and economics.  This is because of its usefulness in modeling non-linear behavior in a linear model, which makes it a driver for tools that are widely used such as Priciple Component Analysis (PCA).

Discussing matrix mulitiplication can help give an overview of the general performance of the data structure and present several of the limitations which were previously discussed.  A great way to become even more familiar with the operation would be to define the operation step by step through function definition and the manipulation of the data structures.  We will take a matrix, let's call it $$A$$, and another matrix called $$B$$ to demonstrate the two operations which will be defined through function definition.

Let's define matrix $$A$$ as:
$$ \begin{bmatrix}
3 & 12 & 7\\
11 & 4 & 0\\
1 & 7 & 6
\end{bmatrix} $$

and let's define matrix $$B$$ as:
$$ \begin{bmatrix}
32 & 1 & 6\\
2 & 7 & 10\\
4 & 11 & 25
\end{bmatrix} $$

and here is the code to initiate the matrices:
```
int matrix_A[3][3] = {
    {3, 12, 7},
    {11, 4, 0},
    {1, 7, 6}
};

int matrix_B[3][3] = {
    {32, 1, 6},
    {2, 7, 10},
    {4, 11, 25}
};
```

## Matrix Multiplication
The function defines the operation to be performed on the matrices that were defined previously as such:
```
void matrixMult(const int A[3][3], const int B[3][3], int result[3][3]) {
    // Initialize result matrix to zero
    for (int i = 0; i < 3; ++i)
        for (int j = 0; j < 3; ++j)
            result[i][j] = 0;

    // Perform multiplication
    for (int i = 0; i < 3; ++i)
        for (int j = 0; j < 3; ++j)
            for (int k = 0; k < 3; ++k)
                result[i][j] += A[i][k] * B[k][j];
}
```
we can then call the function with the following code:
```
matrixMult(matrix_A, matrix_B);
```
