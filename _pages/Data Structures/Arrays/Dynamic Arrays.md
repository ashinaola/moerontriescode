---
title: "Dynamic Arrays: Let's Create and Use One"
date: "2025-05-19"
bookmark: true
thumbnail: "/assets/img/thumbnail/dynamicarray.png"
---

In the introductory post, the concept of static arrays were introduced.  There are several limitations which are associated with static arrays which includes:

>1. a limited amount of space allocated to the array
>2. shifting elements upon insertion and removal

To address the fixed capacity limitation, a pointer can be used to dynamically allocate memory for the array in this way:
```
int *intarr = new int[size];
```
The above line of code declares a pointer to the first element of the integer array called intarr.  This allows for the memory to be allocated on the heap, compared to the stack for static arrays.  However, the limitation with dynamic allocation is that the maximum size needed for the array is unknown to begin with.

A dynamic array can address both previously mentioned problems while also introducing better memory management practices.  The dynamic array also preserves the effecient storage and retrievals of static arrays, allowing storage and retrieval to be constant (O(1)) time.

Let's build a generic template class for a dynamic array, then delve into the some of the operations which set it apart from a typical static array.  Lastly, we will try using the array to store a nondetermined amount of elements to test its flexibility.

# Building the Template Class
To begin building the dynamic array template class, the operations would need to be defined.  Most of the operations from the static array would carry over to the dynamic array class but there are a few additions to the dynamic array class which need to be discussed.  The first operation is a destructor or a way to deallocate the memory from the heap since the memory for the array is allocated through the heap.  The second operation is the `resize()` operation, which checks the array size and expands/shrinks the size as needed.  There are also several differences between the operations to accomodate the dynamic memory allocation and the overhead which it can possibly introduce.

Before diving deeper into the dynamic array class, the design of dynamic array needs to be discussed.  The dynamic array class inherits several attributes and functions from a generic list class called IList.  These attributes and functions can be used by the dynamic array class with some changes to accomodate for heap storage.

## Heap Memory Management
To interact with the heap storage, manual allocation is necessary unlike stack storage where memory is automatically allocated and deallocated. The manual allocation of memory can be carried out using the `new` and `delete` keywords.  While efficient memory management is introduced, there will be an overhead introduced to carry out the allocation. 

There are three attributes which are needed to be introduced to the class to allow the class to interact with heap storage to implement dynamic allocation.  The first attribute is the `arr` which holds the pointer to the dynamically allocated storage area.  When allocating new space for the array, the `new` keyword is used alongside with the array in the constructor.  The second attribute is the `capacity` attribute which represents the total available space in the array.  This is the important attribute which will be used to track the array size to determine whether to expand/shrink the array.  The third attribute is the `size` attribute, which tracks the current number of elements in the array.  This attribute is one of the attributes that are inherited from the IList class and utilized by the dynamic array class.

To carry out the heap memory management, there needs to be three different constructors which take into account the different cases to which the objects can be initiated.  The first is the default constructor, alongside a constructor to be called with a specified capacity and a constructor which declares a capacity and initial value. Here is the code snippets for each constructor:
```
// Default constructor
DynamicArray() : IList<T>(),
arr(new T[getDefaultCapacity]),
capacity(getDefaultCapacity()) {}

// Constructor + capacity(capVal)
DynamicArray(size_t capVal) : IList<T>(),
arr(new T[capVal]),
capacity(capVal) {}

// Constructor + capacity(capVal) + initial value(initVal)
DynamicArray(size_t capVal, const T initVal) : IList<T>(),
arr(new T[capVal]),
capacity(capVal) {}

// Destructor for memory deallocation
virtual ~DynamicArray() {
    delete [] arr;
}
```
Notice the use of the `new` in the constructors and `delete` in the destructor to carry out manual memory management through the inclusion of the previously mentioned attribute members.  After creating the constructors and destructors, the interface functions from the IList class can be defined to control how the DynamicArray objects will behave.  

## resize() Operation
Another major difference between the dynamic and static array definitions is also the `resize()` operation, which checks the size of the array and then grows/shrinks the array based on the amount of elements that are existing on the array.  The `resize()` operation is triggered before an element is inserted if the current size of the array is equivalent to the capacity.  Also, before an element is removed, the array's size is checked to see if the capacity is 3x greater than the array's current size.  This check is implemented in a single line as demonstrated:
```
// on adding an element
assert(i >= 0 && i < size);

// on removing an element
if (capacity >= 3 * size){}
```
To implement the operation, the `resize()` function is implemented in 4 general steps:
> 1. Initiate a new value for the capacity of the new array
> 2. Initiate a pointer to the new array
> 3. Copy the elements in the old array to the new array
> 4. Destroy the old array and set the capacity to the new capacity

These four steps can be incorporated into the insert and remove operations to ensure proper memory management is baked into the implementation of the DynamicArray class.  The complete `resize()` function for the dynamic array is as follows:
```
void DynamicArray<T>::resize() {
    // initiate new val for capacity
    size_t new_capacity = std::max(2*static_cast<int>(size), 2);

    // initiate a ptr to new arr
    T* new_arr = new T[new_capacity];

    // Copy elements to new arr
    for (size_t i = 0; i < size; i++)
        new_arr  = arr[i];
    
    // Destroy old arr and set cap to new_arr
    delete[] arr;
    arr = brr;
    capacity = new_capacity;
}
```

## Ways to Optimize the `resize()` Operation
While the code that was written carries out the `resize()` operation, it can become a problem when the size of the array starts to grow to a larger size.  As the amount scales up, there might need to be some optimization of the overhead that dynamic arrays present when copying the array over to the new array.  One way of optimizing the for loop in the function is to use `std::copy()` function to copy the elements to the new array.  This optimization takes advantage of the provided copy algorithm which uses machine instructions to copy the elements over.

>Quick Overview of `std::copy()`
>The copy algorithm provided by C++ takes three different parameters and is in the format copy(start, finish, element) where start and finish defines the index range of the copy and the object is the address of the object where the elements should be copied to.  C++ also provides other algorithms which can also act on overlapping ranges such as `std::copy_backwards()`

An optimized version of the `resize` operation replaces the for loop with the copy algorithm as follows:
```
void DynamicArray<T>::resize() {
    size_t new_capacity = std::max(2 * static_cast<int>(size), 2);
    T* new_arr = new T[new_capacity];
    std::copy(arr, arr + size, new_arr);
    delete[] arr;
    arr = new_arr;
    capacity = new_capacity;
}
```
