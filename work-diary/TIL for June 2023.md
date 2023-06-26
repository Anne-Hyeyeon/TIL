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



# 2023-06-19 (Came back from my honeymoon!!!)
## Rendered more hooks than during the previous render. Why does this error occur? 
- The error message "Rendered more hooks than during the previous render" typically occurs in React when you have a mismatch in the **number or order of hooks used** within a component.
-  Hooks in React, such as useState or useEffect, must always be called in the same order and quantity on every render of a component.

### This error commonly happens when:
1. `Hooks are conditionally called`: If you have hooks inside conditional statements (like if statements or loops), ensure that they are called unconditionally on every render path. Hooks should be called in the same order on every render, and conditional statements can cause inconsistencies.
2. `Hooks are called inside nested functions or loops`: Hooks should only be called directly inside functional components or custom hooks, not within nested functions or loops. Make sure the hooks are called directly within the component's body.
3. `Hooks are used in wrong components`: Each component should have its own separate set of hooks. If you accidentally use hooks inside **child components or helper functions**, it can result in the "Rendered more hooks" error.

### To resolve this error:
- Ensure that you consistently call hooks **in the same order and quantity on every render of your component.** Check for any **conditional statements or nested functions** that might be causing the issue. Also, ensure that hooks are **used only in functional components or custom hooks**, not in nested functions or loops.

# 2023-06-20
## 10 Topics for Intermediate Front-End Developer

1. `Responsive Web Design`: Explore how to develop web designs that adapt to various devices and screen sizes using media queries.
2. `CSS Preprocessors (Sass, Less)`: Introduce the usage of CSS preprocessors to enhance code reusability and maintainability.
3. `CSS Grid System`: Share techniques and tips for utilizing CSS grid to construct web page layouts effectively.
4. `Modern JavaScript`: Demonstrate writing more efficient and concise code using JavaScript features from ES6 and beyond.
5. `Web Accessibility`: Discuss techniques for adhering to web accessibility guidelines, ensuring easy access for all users. ⭐⭐
6. `Performance Optimization`: Address methods to improve website loading speed and overall performance, such as image optimization, code bundling, and caching. ⭐⭐⭐
7. `Mobile Web Development`: Present technologies related to developing mobile-optimized web apps or sites.
8. `Frontend Frameworks`: Introduce frontend frameworks like React, Vue.js, Angular, and provide simple examples or use cases.
9. `Responsive Images`: Cover methods for providing optimized images that adjust to different screen sizes, including srcset and sizes attributes, image resizing, and more.
10. `Web Security`: Introduce fundamental web security concepts that frontend developers should be aware of, along with mitigation techniques and best practices. ⭐⭐⭐

- I am weak in all areas, but the ⭐ indicates  that I need to put extra effort into.


- Recently, I have been working on adding horizontal scrollbars to my components. Here is some CSS knowledge related to the task I have been working on.
# 2023-06-22
## calc()
### calc()?
-  calc() function in CSS allows you to perform **mathematical calculations within property values.** It provides a convenient way to **dynamically calculate** and set values based on arithmetic expressions.
### How can I use calc()?
- The calc() function accepts various mathematical operators such as addition (+), subtraction (-), multiplication (*), and division (/).
- It can operate on different types of CSS units, including **lengths (pixels, percentages, ems, rems)**, **angles (degrees, radians)**, and even some **color-related values.**
- You can use calc() to combine fixed values with dynamic values, perform calculations based on different properties, or create responsive layouts.

```css
.container {
  width: calc(50% - 20px); /* Calculates the width to be 50% minus 20 pixels */
  height: calc(100vh - 2rem); /* Calculates the height to be the full viewport height minus 2 rems */
  font-size: calc(12px + 2vw); /* Calculates the font size based on a base size of 12 pixels plus 2% of the viewport width */
}
```
- Be sure to check the browser compatibility for the properties and values you're using calc() with.

# 2023-06-23
## overflow: auto
- The "overflow: auto" property is used to control how content that exceeds the dimensions of an element should be displayed.
- When applied to an element, it enables scrollbars to appear when necessary, allowing users to scroll and view the overflowing content.

### The conditions that determine when scrollbars will appear:
1. `Content Size`: Scrollbars will only appear if the content inside the element **exceeds its specified dimensions.** This includes both the **width** and **height** of the element. If the content fits within the element without overflowing, no scrollbars will be displayed.

2. `Element Size`: The element itself must have a **defined size** in order for scrollbars to appear. This can be achieved by **setting explicit width and height values** or by using CSS properties such as **"min-width"**, **"max-width"**, **"min-height"**, or **"max-height"**.

3. `Overflow`: The content must be set to **overflow the boundaries of the element.** The "overflow" property can have four possible values: "visible" (default), "hidden", "scroll", or "auto". To enable scrollbars, the value should be set to "auto" or "scroll". "auto" allows the scrollbars to appear only when needed, while "scroll" forces the scrollbars to always be visible.

4. `Parent Container`: If the element with "overflow: auto" is nested inside another container, such as a div, **the parent container should have a defined size as well**. If the parent container is too small to accommodate the child element with overflow, scrollbars will appear on the parent container, allowing scrolling within the child element.

- In summary, when using "overflow: auto", scrollbars will appear if the content inside the element overflows its dimensions, the element itself has a defined size, the "overflow" property is set to "auto" or "scroll", and the parent container, if present, has a sufficient size to contain the child element with overflow.


# 2023-06-26
## height: 100%
### 😭
- I recently realized that my understanding of height: 100% was incorrect. As a frontend developer, it's crucial to have a solid grasp of fundamental concepts. Unfortunately, I misunderstood how height: 100% works in relation to child elements. I mistakenly believed that the height of a child element would be determined by setting height: 100% on its parent.

- In reality, height: 100% is a way to make an element's height match its parent element's height. It doesn't depend on the content or size of the child elements. Similarly, width: 100% sets the width of an element to be equal to its parent element's width.

- I now realize that it's essential to have a clear understanding of these concepts to write effective frontend code. I apologize for any confusion my previous understanding may have caused, and I'm committed to continuously improving my skills as a frontend developer.

### height: 100%
- `width: 100%` means that the width of the element is set to be the **same as its parent element's width**. In other words, it takes up 100% of the parent element's width relative to it.
- `height: 100%` means that the height of the element is set to be the **same as its parent element's height**. In other words, it takes up 100% of the parent element's height relative to it.

- By using these two properties, you can adjust the size of an element to match its parent element. For example, if the parent element has a width of 500px, setting width: 100% on the child element will also make it have a width of 500px. Similarly, if the parent element has a height of 300px, setting height: 100% on the child element will also make it have a height of 300px.

### 100vh
- `100vh` represents **100% relative to the viewport height**. The viewport refers to the visible area of the browser window that the user is currently viewing. Therefore, when you use height: 100vh, the element's height will be set to be the same as the **current height of the browser window.** This is useful for making an element expand to occupy the full height of the browser window, including the scrollable area.

### In summary:
- `width: 100% and height: 100%` adjust the size of the child element relative to its parent element.
- `100vh` adjusts the size of the element relative to the current height of the browser window.
