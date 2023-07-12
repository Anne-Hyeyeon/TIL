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

# 2023-07-07
## Using `ternary operator` vs `&&`
- While refactoring my code, I was debating whether to replace && with the ternary operator .
```tsx
// original code
...
return (
  {data && (...)}
  {!data && (...)}
)
```
The reason I wrote the code in this way is that I find it takes more time to understand the intention of the code when using the ternary operator. I believe that using `&&` allows me to convey my intention more intuitively by clearly indicating the conditions of "there is data" and "there is no data."
```tsx
// refactored code
...
return (
  {data ? (...) : (...)
)
```
However, in the end, I have decided to change && to the ternary operator.

### why I changed `&&` to termary operator

- sing the && operator instead of the ternary operator for the conditional rendering of the data section generally should not cause any issues. The && operator is also known as **"short-circuit evaluation,"** where it stops evaluation and returns false if the condition is false. Therefore, if data is absent, it will be considered falsy and that part will not be rendered.
- However, it is important to note that this approach is applicable only when data is `null` or `undefined`. If data can be other falsy values like `false`, `0`, or an empty string, but they should still be considered valid data, using the && operator may lead to incorrect rendering. In such cases, it is safer to use the ternary operator to explicitly handle the condition.
- Therefore, if I only want to render that section when data is null or undefined, using the && operator should be fine. Otherwise, when dealing with other falsy values, it is recommended to use the ternary operator for explicit handling.


# 2023-07-11
## Middlewares
- middleware refers to software or infrastructure that **sits between** different applications, systems, or components, enabling communication, integration, and coordination. It abstracts the underlying complexities and provides a unified interface or services that facilitate interoperability, scalability, and reliability in distributed environments.
  
### `RPC (Remote Procedure Call)`
RPC is a communication protocol that allows a program to **call functions or procedures on a remote system as if they were local**. It enables the client and server applications to communicate **across different machines** or networks transparently. The client program invokes a procedure on the server, and the RPC mechanism handles the underlying network communication and marshaling of data.

### `MOM (Message-Oriented Middleware)`
MOM is a middleware infrastructure that supports the **exchange of messages between distributed applications.** It provides a communication model based on **asynchronous message passing**, where applications can send and receive messages independently of each other. MOM ensures reliable delivery, message queuing, and often supports features like publish/subscribe and message filtering.

### `ORB (Object Request Broker)`
ORB is a middleware component that **facilitates communication between distributed objects in a distributed system**. It enables objects written in **different programming languages to interact transparently** by providing services such as object location, method invocation, and parameter marshaling. ORB acts as an intermediary between clients and servers, handling the complexities of distributed object communication.

### `DB middleware (Database Middleware)`
DB middleware refers to software components or services that **sit between applications and databases**, providing an **abstraction layer and facilitating database connectivity**. It simplifies database access for applications by handling tasks like connection management, query execution, transaction management, and data caching. DB middleware often includes features like object-relational mapping (ORM) and database connection pooling.

### `TP monitor (Transaction Processing Monitor)`
TP monitor is a middleware system designed to **manage and coordinate transactional processing** in distributed environments. It provides services for transaction management, concurrency control, resource allocation, and recovery. TP monitors ensure the integrity and consistency of distributed transactions across multiple systems or databases.

### `WAS (Web Application Server)`
WAS is a middleware platform specifically designed to **host and manage web applications**. It provides a runtime environment that supports the **execution of web-based applications**, including handling **HTTP requests** managing application components, and providing services like security, session management, and scalability. WAS typically includes **a web server, servlet engine, and support for various web technologies**.



# 2023-07-12
## Denormalization
- Denormalization is a technique in database design where certain principles of **normalization are deliberately violated** in order to **improve performance**.
  While normalization aims to **eliminate data redundancy** and **ensure data consistency and integrity**, there are situations where optimizing **read and write operations** becomes more important.

1. `Adding duplicate tables`: One form of denormalization is **adding tables** that contain **duplicated data**. This **sacrifices data consistency** but improves the **performance of read operations**. For example, when there are separate tables for orders and customers, duplicating customer name and address in the orders table can expedite queries that require customer information.

2. `Combining tables` : Another form of denormalization involves **combining multiple tables into one**. This allows retrieving related data in a single query, thereby **enhancing performance**. For instance, combining the order table and product table allows retrieving information about ordered products more efficiently.

3. `Eliminating splits` : Denormalization sometimes involves **reversing the splits caused by normalization**. In a normalized database, querying data often requires joining multiple tables, which can degrade performance. In such cases, denormalization involves merging the normalized tables back into one, leading to performance improvements.

- It's important to exercise caution when applying denormalization. **Increased data redundancy** requires additional efforts to **maintain data consistency**, and updating duplicated data consistently becomes crucial. Additionally, denormalization is a performance-oriented technique, so its application should be carefully considered based on the specific circumstances.

## Schema in Database System
1. `External Schema` : The external schema defines **how users or applications interact with the database**. For example, in a bank, there are three groups of people: bank tellers, customers, and managers, each using the bank system in different ways. The external schema would define the information that tellers see, what customers see, and what managers see. Bank tellers may need to view and process account transactions, customers may need to check their account balance and transaction history, while managers may need access to comprehensive reports.

2. `Conceptual Schema` : The conceptual schema represents **the overall structure of the database**. It describes all the data and their relationships within the database. For instance, a database may contain various bank accounts and associated transaction records. The conceptual schema defines how these **accounts and transactions are stored and related to each other**. It ensures that multiple users and applications can share the database while maintaining data consistency. The conceptual schema is typically represented using models like ER diagrams or UML diagrams.

3. `Internal Schema`: The internal schema defines the `physical structure of the database`. It specifies the actual format of data stored on **disk**, **storage methods**, index **structures**, and other low-level details. The internal schema deals with the internal workings and performance aspects of the database system. Generally, it is managed by the database system itself, and users or applications do not directly interact with it.
