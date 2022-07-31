# Minimal Browser

This is a browser built entirely from scratch in a single file of Python - meaning it implements its own HTML/CSS parser and draws and renders everything in a GUI window manually. 

I built this to better understand browsers at a fundamental level - as web developers we use browsers extensively but I would have been at a complete loss if asked to explain any lower level concepts relevant to them. Building applications using frameworks like React and Vue exclusively, I had no real understanding of how the basic building blocks - HTML and CSS were parsed and rendered. So, I built this to try to gain a deep understanding of how browsers accomplish this very fundamental task.

Since I built my own HTML/CSS parser, this browser implements a very small subset of the actual web standards. The web standards for Google Chrome, for example, is over 114 million lines long. This would be impossible for me to implement - so I have tried to select a very small subset of these that can still render text based websites well and enable basic navigation, while offering tabbed browsing. 

This also means that all websites will not work well - when my browser encounters something that I have not implemented in my parser, it will simply render the code as is and continue. A good indication of whether a website will work with this browser is if command line browsers like Lynx can display it properly - so most blogs and wikipedia articles will work fine and be navigable - any complex web apps that rely heavily on JavaScript will not. This is best viewed as an educational project - I would not recommend anyone try to replace their browser with this. 

## Features: 

Below, I describe chronologically each of the features that I implemented. 

1. **Connecting to a server and downloading web pages**: parse a URL into its constituent components and identify the host, connect to that host using the Python libraries `sockets` and `ssl`, send an HTTP request to that host, split the response we get from the server into its constituent components; finally extract the text from the body.
2. **Rendering this data onto a graphical window**: The browser uses the `tkinter` library to create a window, lays out the text it extracted from the HTTP response into that window, constantly listens for keyboard commands and scrolls the window in response to those keyboard commands.
3. **Better, more human readable text rendering**: Split lines at word boundaries and enable text styling and sizing. 
4. **HTML parser**: Transform the HTML tokens from the HTTP response body into a tree, recognize and handle the different attributes on the different HTML elements, provide sane defaults and automatic fixes if some HTML tokens cannot be identified/read, and build out a recursive algorithm that can span and navigate through this tree. 
5. **Recursive layout**: Span through the HTML tree using the recursive algorithm and produce a layout tree - each layout object has a definite size and position within the graphical window of the browser. Additional formatting added for any code snippets that end up being rendered as text to enable easy distinction. 
6. **CSS Parser**: Support for both linked CSS files and the inline `style` attribute in HTML tags, added support for cascading and inheritance and built a separate style sheet `browser.css` that handles the basic settings for the browser itself. 
7. **Hyperlinks, tabbed browsing, address bar, back button**: Added support for navigating to and from pages using hyperlinks, and implemented various UI improvements inspired by modern browsers - multiple tabs can now show multiple web pages, an address bar allows direct typing of web addresses instead of rebuilding the browser with a different URL, and a back button allows navigating through the history of pages visited. 

## Installation and running local instance:

Clone this project, install `tkinter` if you have not already using `pip3 install tk` (ideally in a virtual environment) and run `./runBrowser.sh` in the `src/` directory of the project. This will open the browser, pointing to the wikipedia page for web browsers. If you would like to change the homepage, simply type the URL after the shell command. For example, to open the browser at `https://www.example.org`, run `./runBrowser.sh https://www.example.org`. 

## Roadmap: 

I found significant parallels in building a parser for HTML and CSS, and in building interpreters for other Domain Specific Languages - the main difference arising in that the result of the parsing had to contribute to some clear visual element whereas when building an interpreter for a regular programming language we are usually done after building some sort of AST and identifying a way to recurse through it. It was, in that sense, unlike anything I had attempted before and I am very glad that I undertook this. 

The current supported functionality is very basic and I would love to extend it. I am starting by adding support for forms to directly interact with web servers beyond just obtaining the initial HTTP response to render the page, and also looking into adding direct JavaScript support and rendering pages by manipulating the DOM. Eventually, I hope to use the skills that I have gained building this to contribute to projects like Chromium. 