# 2023-06-02
## Server-Side Rendering (SSR)
- Server-Side Rendering involves rendering the web page or application on the server **before sending it to the client**.  
### how it works
1. `Initial request`: The client sends a **request to the server** for the web page or application.
2. `Server rendering`: The server retrieves the necessary data, performs the rendering process (including dynamic content generation), and generates a **complete HTML response.**
3. `Client response`: The server sends the **fully rendered HTML page** to the client, including all the content, styles, and interactivity.
4. `Interactivity`: Once the client receives the HTML, it becomes interactive immediately, and subsequent user interactions may trigger API requests to update specific parts of the page.
### Pros of SSR
- `Faster initial load`: Since the server sends a complete HTML response, the **initial load time is usually faster** as the client **doesn't need to execute JavaScript** to render the page.
- `SEO-friendly` : **Search engines can easily index the fully rendered HTML**, improving discoverability and SEO.
- `Graceful degradation`: SSR provides a fallback for clients that don't support JavaScript or have it disabled.

### Cons of SSR
- `Slower subsequent navigation`: Navigating between pages or sections may require full page reloads, as the server needs to render each new request.
- `Increased server load`: Rendering on the server adds processing load, as it has to generate the HTML for each request.

# 2023-06-08
## React's component lifecycle 
- React components go through various phases during their lifecycle, and each phase has lifecycle methods that can be implemented to perform certain actions. 
- The lifecycle can be divided into three main phases: `mounting`, `updating`, and `unmounting`.
- 
### Mounting Phase
1. `Constructor`: This is the first method called when an instance of a component is created. It is used to **initialize state** and **bind event handlers.
2. `Static getDerivedStateFromProps`: This static method is called before rendering and allows the component to update its internal state based on changes in props. It returns an object to update **the state or null** to indicate no state update is needed.
3. `Render` : The render method is responsible for returning the **JSX** that represents the component's UI.
4. `ComponentDidMount` : This method is invoked immediately after the component is **inserted into the DOM**. It is commonly used to initiate API calls, set up subscriptions, or perform other **initialization tasks** that require access to the DOM.

### Updating Phase
1. `Static getDerivedStateFromProps`: This method is also called during the updating phase, just like in the mounting phase. **It allows the component to update its state based on changes in props.** It has the same usage as in the mounting phase.
2. `ShouldComponentUpdate` : This method is called before the component re-renders, allowing you to control whether the re-rendering should occur or not. By default, it returns true, indicating that the component should update. However, you can optimize performance by implementing custom logic here to determine if an update is necessary.
3. `Render` : The render method is called again to re-render the updated UI based on new props or state.
4. `ComponentDidUpdate` : This method is invoked immediately after the component is updated in the DOM. It can be used to perform side effects such as **making additional API calls** or **updating the DOM** in response to prop or state changes. You should be cautious when updating state within this method to **avoid infinite update loops.


### Unmounting Phase
1. `ComponentWillUnmount` : This method is called just before the component is **removed from the DOM.** It is used to perform any necessary cleanup, such as **canceling API requests, removing event listeners, or clearing timers.

- It's important to note that with the introduction of React Hooks, the lifecycle methods can also be implemented in functional components using the useEffect and other hook functions.
- Not all lifecycle methods need to be implemented in every component. You can choose the appropriate methods based on the specific needs of your component.



# 2023-06-16 (Came back from my honeymoon!!!)
## Rendered more hooks than during the previous render. Why does this error occur? 
- The error message "Rendered more hooks than during the previous render" typically occurs in React when you have a mismatch in the **number or order of hooks used** within a component.
-  Hooks in React, such as useState or useEffect, must always be called in the same order and quantity on every render of a component.

### This error commonly happens when:
1. `Hooks are conditionally called`: If you have hooks inside conditional statements (like if statements or loops), ensure that they are called unconditionally on every render path. Hooks should be called in the same order on every render, and conditional statements can cause inconsistencies.
2. `Hooks are called inside nested functions or loops`: Hooks should only be called directly inside functional components or custom hooks, not within nested functions or loops. Make sure the hooks are called directly within the component's body.
3. `Hooks are used in wrong components`: Each component should have its own separate set of hooks. If you accidentally use hooks inside **child components or helper functions**, it can result in the "Rendered more hooks" error.

### To resolve this error:
- Ensure that you consistently call hooks **in the same order and quantity on every render of your component.** Check for any **conditional statements or nested functions** that might be causing the issue. Also, ensure that hooks are **used only in functional components or custom hooks**, not in nested functions or loops.
