# 2023-07-03
## White Box Testing And Black Box Testing
White Box Testing and Black Box Testing are two commonly used testing techniques in software development. They differ in terms of the level of knowledge about the internal workings of the system being tested.

### White Box Testing
- White Box Testing, also known as **Clear Box Testing or Structural Testing**, is a testing approach where **the tester has access to the internal structure, code, and implementation details of the software system.** 
- The purpose of White Box Testing is to **evaluate the internal logic and flow of the system**, as well as to ensure that **all code paths** are properly executed and tested. Test cases are designed based on the internal structure of the software.
#### example
- Let's say you are testing a function that calculates the square root of a number. In White Box Testing, you would have knowledge of the code implementation of the function. You would design test cases that cover different code paths, such as testing with positive numbers, negative numbers, zero, and invalid input. You might also include test cases to ensure the function handles edge cases correctly, such as very large or very small numbers.

### Black Box Testing
- Black Box Testing is a testing approach where **the tester does not have access to the internal structure, code, or implementation details of the software system.**
- The tester focuses solely on the **inputs and outputs of the system**, without any knowledge of its internal workings. Black Box Testing aims to **evaluate the system's behavior and functionality** based on its specifications, requirements, and expected outputs.
#### example
Let's consider testing a login functionality of a website. In Black Box Testing, you would only have access to the **user interface and specifications.** You would design test cases based on the expected behavior of the login feature, such as verifying if valid usernames and passwords are accepted, checking for error messages with invalid inputs, testing password reset functionality, and ensuring proper redirection after successful login. You would not have knowledge of the code implementation or the internal workings of the authentication process.

### conclusion
Both White Box Testing and Black Box Testing have their advantages and are used in different scenarios. White Box Testing is useful for thorough code coverage and identifying internal defects, while Black Box Testing focuses on validating the system's functionality from an end-user perspective. Often, a combination of both techniques is employed to achieve comprehensive test coverage.

# 2023-07-04
## Sorting Algorithms
### `Bubble Sort`
- It compares **adjacent elements** in the array and **swaps their positions** if necessary. Bubble Sort is the simplest but least efficient algorithm, especially for large arrays.
- time complexity(average) : O(n^2)
### `Selection Sort`
- It finds the **smallest element** in the given array and swaps it with the first position. Then, it finds the second smallest element and **swaps** it with the second position. Selection Sort is not efficient for large arrays because it repeatedly searches for the minimum value.
- time complexity(average) : O(n^2)
### `Insertion Sort`
- It divides the array into a **sorted and an unsorted part**. It takes the first element from the unsorted part and inserts it into the sorted part in the appropriate position. Insertion Sort is efficient for small-sized arrays.
- time complexity(average) : O(n^2)
### `Quick Sort`
-  It uses the **divide and conquer approach** to sort the array. Quick Sort selects **a pivot from the array**, places the **smaller elements to the left of the pivot**, and the **larger elements to the right**. It recursively performs Quick Sort on each subarray. Quick Sort is efficient in most cases.
- time complexity(average) : O(nlogn)
### `Merge Sort `
- It uses the **divide and conquer approach** to sort the array. Merge Sort **divides the array into halves**, recursively sorts each half, and then **merges the sorted halves to obtain the fully sorted array**. It is a stable sorting algorithm and efficient for large datasets.
- - time complexity(average) : O(nlogn)
### `Heap Sort`
- It sorts the array **based on a complete binary heap data structure**. Heap Sort constructs **a max heap or min heap** from the given array, then extracts the **root node and stores it from the back of the array**. The extracted node is removed, and the heap is restructured. Heap Sort has a time complexity of **O(nlogn)** even in the worst case.
- time complexity(average) : O(nlogn)

# 2023-07-06
## Design patterns
- Design patterns provide reusable solutions to **common problems in software design, promoting flexibility, extensibility, and maintainability.** They help in achieving consistency and enhancing various aspects of software development.
### `Bridge Pattern`
- The Bridge pattern **separates abstraction from implementation**, allowing them to vary independently.
- It defines an interface between the **abstraction and the implementation**, and implements them as separate classes. This reduces the coupling between the abstraction and implementation and provides a flexible connection between two hierarchies.

### `Visitor`
- The Visitor pattern allows adding **new operations to an object structure without modifying it**.
- It separates the **operation from the object structure**.
- To add a new operation, a concrete Visitor class implementing the Visitor interface is created, defining the operation for each element of the object structure.
- This way, the **object structure remains unchanged** while new operations can be applied to it.

### `Observer`
- The Observer pattern defines a **one-to-many dependency between objects**, where multiple observers are **notified automatically of any state changes** in the subject.
- When the state of the subject changes, it notifies all its observers. 🌟
- This **reduces the coupling between the subject and observers**, enabling loose coupling and interaction.
- The Observer pattern is commonly used in event handling, MVC architecture, publisher/subscriber model, etc.

