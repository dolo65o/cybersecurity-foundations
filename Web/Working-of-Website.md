## How websites work

When you visit a website, your browser (like Safari or Google Chrome) makes a request to a web server asking for information about the page you're visiting. It will respond with data that your browser uses to show you the page.

There are two major components that make up a website:

1. Front End (Client-Side) - the way your browser renders a website.
2. Back End (Server-Side) - a server that processes your request and returns a response.

Websites are primarily created using:

* HTML, to build websites and define their structure
* CSS, to make websites look pretty by adding styling options
* JavaScript, implement complex features on pages using interactivity

## HTML

HyperText Markup Language (HTML) is the language websites are written in. Elements (also known as tags) are the building blocks of HTML pages and tells the browser how to display content.

```
<!DOCTYPE html>
<html>
  <head>
    <title>Page Title</title>
  </head>
  <body>
    <h1>Example Heading</h1>
    <p>Example paragraph..</p>
  </body>
</html>
```

Basic HTML Structure: 

- `<!DOCTYPE html>` — Declares the doc as HTML5.
- `<html>` :- Root of the HTML page.
- `<head>` :- Metadata, title, links to CSS/scripts.
- `<body>` :- Main content shown in browser.
- `<h1>` :- Big heading (used for titles).
- `<p>` :- Paragraph text.
  
> Tags like `<button>`, `<img>`, `<ul>`, etc., are used for different features.

HTML Attributes:

- class — Used for styling (CSS). E.g. `<p class="bold-text">`
- id — Unique identifier for one element. E.g. `<p id="example">`
- src — Specifies image path. E.g. `<img src="img/cat.jpg">`
> You can use multiple attributes inside a tag.

## JavaScript (JS) 

HTML is used to create the website structure and content, while JavaScript is used to control the functionality of web pages - without JavaScript, a page would not have interactive elements and would always be static. JS can dynamically update the page in real-time, giving functionality to change the style of a button when a particular event on the page occurs (such as when a user clicks a button) or to display moving animations.

### How to Add JS
- Inline script:
    ```
    <script>
      document.getElementById("demo").innerHTML = "Hack the Planet";
    </script>
    ```
- External file:
   ```
      <script src="/location/of/javascript_file.js"></script>
   ```

### DOM Manipulation
- JS can target elements using:
   ```
    document.getElementById("demo").innerHTML = "Hack the Planet";
   ```
### JS Events
- Example: run code when a button is clicked:
  ```
  <button onclick='document.getElementById("demo").innerHTML = "Button Clicked";'>Click Me!</button>
  ```

## HTML injection

HTML Injection is a web security vulnerability that occurs when a web application includes unvalidated or unsanitized user input directly in the HTML output.

- How It Works
    - Attackers input raw HTML (e.g., through a form or URL parameter).
    - If the application fails to sanitize or escape it, that HTML is rendered by the browser.
    - This injected HTML becomes part of the page, leading to unintended behavior.
 
- Risks and Impact
    - Can be used to alter webpage structure or content.
    - May lead to Cross-Site Scripting (XSS), where malicious JavaScript is executed in the victim’s browser.
    - Enables data theft, session hijacking, and phishing attacks by modifying the UI or injecting fake elements.
 
- Prevention Techniques
    - Validate all user input to ensure it conforms to expected formats.
    - Sanitize output by escaping HTML tags and attributes.
    - Use well-tested security libraries or frameworks that handle output encoding.
    - Apply Content Security Policy (CSP) as an extra mitigation layer. 
