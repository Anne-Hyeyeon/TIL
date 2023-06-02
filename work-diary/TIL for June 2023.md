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
