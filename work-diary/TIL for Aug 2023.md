# 2023-08-03
## Middlewares - RPC
### What is RPC (Remote Procedure Call)?
`Remote Procedure Call (RPC)` is a **communication protocol** and **programming paradigm** used in distributed computing environments. The main idea behind RPC is to allow programs or processes running on different machines to communicate with each other as if they were local procedures or functions. It abstracts the complexity of remote communication and provides a way to invoke functions on a remote server in a manner that appears almost identical to invoking a local function.
### Key Points of RPC
`Abstraction of Remote Calls`: RPC provides an abstraction layer that hides the underlying networking and communication details. Developers can call remote functions or procedures in a way that is conceptually similar to invoking local functions.

`Client-Server Interaction`: RPC typically involves a client-server architecture, where the client sends a request to the server to execute a specific function. The server performs the requested operation and sends the result back to the client.

`Stubs and Skeletons`: To achieve the illusion of local function calls, RPC uses stubs (on the client side) and skeletons (on the server side). The client-side stub packages the request parameters and sends them to the server, while the server-side skeleton unpacks the request, executes the function, and sends the result back.

`Interface Definition`: An important aspect of RPC is defining the interface of the remote procedures. This includes specifying the methods, their parameters, and return values in a language-independent way using an interface definition language (IDL).

`Binding`: The process of connecting a client to a specific server implementing the remote procedures is known as binding. There can be different binding techniques, such as static binding (where the client knows the server's location) and dynamic binding (where a separate service helps locate the server).

`Synchronous and Asynchronous Calls`: RPC supports both synchronous and asynchronous communication. In synchronous RPC, the client waits for the server's response before continuing. In asynchronous RPC, the client can continue its work while waiting for the response.

`Security and Error Handling`: Security mechanisms can be integrated into RPC to ensure secure communication between client and server. Error handling is also an important aspect, as network failures or remote server unavailability should be gracefully managed.

`Use Cases`: RPC is used in various scenarios, including distributed systems, client-server applications, and microservices architectures, where different components need to communicate across network boundaries.
