# JavaScript Basics — Variables, Data Types, Functions & Loops

## Variables

Variables are **containers** that store data values.
Each variable has a name so it can be referenced later.

### Three Ways to Declare Variables in JS

| Keyword | Scope | Can Reassign? | Use When |
|---------|-------|---------------|----------|
| `var` | Function-scoped | Yes | Older code (avoid in modern JS) |
| `let` | Block-scoped | Yes | Value will change |
| `const` | Block-scoped | No | Value will NOT change |

> `let` and `const` are preferred** over `var` in modern JavaScript — they offer better control over variable visibility within specific code blocks

### Examples
```javascript
var name = "Dolo";           // function-scoped
let score = 95;              // block-scoped, can change
const maxScore = 100;        // block-scoped, cannot change
```

---

## Data Types

Data types define what **type of value** a variable holds.

| Data Type | Example | Description |
|-----------|---------|-------------|
| `string` | `"Hello"` | Text values |
| `number` | `42`, `3.14` | Numeric values |
| `boolean` | `true`, `false` | True or false only |
| `null` | `null` | Intentionally empty |
| `undefined` | `undefined` | Variable declared but not assigned |
| `object` | `{name: "Jon"}` | Complex data, arrays, objects |

```javascript
let username = "Dolo";          // string
let age = 20;                   // number
let isLoggedIn = true;          // boolean
let emptyValue = null;          // null
let notAssigned;                // undefined
const user = {name: "Dolo"};   // object
```

---

## Functions

A function is a **block of code** designed to perform
a specific task. Group similar logic together and
call it whenever needed.

### Example — PrintResult Function
```javascript
<script>
    function PrintResult(rollNum) {
        alert("Username with roll number " + rollNum + " has passed the exam");
        // any other logic to display the result
    }

    // prepare an array of roll numbers (data)
    const rollNumbers = [101, 102, 103];

    for (let i = 0; i < 100; i++) {
        PrintResult(rollNumbers[i]);
    }
</script>
```

> Instead of writing `PrintResult()` 100 times manually, we define it **once** and call it inside a loop

---

## Loops

Loops run a **code block multiple times** as long as
a condition is `true`.

### Common Loop Types in JavaScript

| Loop | Use When |
|------|----------|
| `for` | You know how many times to repeat |
| `while` | Repeat while condition is true |
| `do...while` | Run at least once, then check condition |

---

## Full Example — Putting It All Together

```javascript
<script>
    // Function to print student result
    function PrintResult(rollNum) {
        alert("Username with roll number " + rollNum + " has passed the exam");
        // any other logic to display the result
    }

    // prepare an array of roll numbers (data)
    const rollNumbers = [101, 102, 103];

    // Note: We only have 3 roll numbers,
    // so after i = 2, rollNumbers[i] becomes undefined

    for (let i = 0; i < 100; i++) {
        PrintResult(rollNumbers[i]); // this will be called 100 times
    }
</script>
```
---

# JavaScript — Integrating JS into HTML

## Overview

JavaScript works **alongside HTML and CSS** to create
dynamic and interactive web pages. JS is not used to
render content — it adds behaviour and interactivity.

There are **two main ways** to integrate JS into HTML:
1. Internal JavaScript
2. External JavaScript

---

## Internal JavaScript

JS code written **directly inside** the HTML document
between `<script>` tags.

> Preferable for beginners — easy to see how the script interacts with the HTML on the same page

### Where to place `<script>` tags

| Location | When to use |
|----------|-------------|
| Inside `<head>` | Scripts that must load **before** page content |
| Inside `<body>` | Scripts that interact with elements **as they load** |

### Example — Internal JS

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <title>Internal JS</title>
</head>
<body>
    <h1>Addition of Two Numbers</h1>
    <p id="result"></p>

    <script>
        let x = 5;
        let y = 10;
        let result = x + y;
        document.getElementById("result").innerHTML = "The result is: " + result;
    </script>
</body>
</html>
```

**What happens:**
```
x = 5, y = 10
result = 5 + 10 = 15
Page displays: "The result is: 15"
```

### Key Line Explained
```javascript
document.getElementById("result").innerHTML = "The result is: " + result;
```

| Part | Meaning |
|------|---------|
| `document` | The entire HTML page |
| `getElementById("result")` | Find element with `id="result"` |
| `.innerHTML` | Set the HTML content inside it |
| `= "The result is: " + result` | Write this text into the element |

---

## External JavaScript

JS code stored in a **separate `.js` file** and linked
to the HTML document using the `src` attribute.

> Keeps HTML clean and organised JS file can be hosted on same server or external CDN

### Step 1 — Create `script.js`

```javascript
let x = 5;
let y = 10;
let result = x + y;
document.getElementById("result").innerHTML = "The result is: " + result;
```

### Step 2 — Create `external.html` and link the JS file

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>External JS</title>
</head>
<body>
    <h1>Addition of Two Numbers</h1>
    <p id="result"></p>

    <!-- Link to the external JS file -->
    <script src="script.js"></script>
</body>
</html>
```

> The `src` attribute in `<script src="script.js">` tells the browser to load JS from the external file

---

## Internal vs External JS — Comparison

| Feature | Internal JS | External JS |
|---------|-------------|-------------|
| Location | Inside HTML file | Separate `.js` file |
| Tag used | `<script>` | `<script src="file.js">` |
| Best for | Beginners, small scripts | Production, larger projects |
| HTML cleanliness |  Mixed with HTML |  Clean separation |
| Reusability |  One page only |  Share across multiple pages |
| Caching |  Not cached |  Browser can cache `.js` file |

---

## Verifying Internal or External JS (Pentesting Tip)

When pen-testing a web application, always check whether
the site uses **internal or external JS** — external JS
files may contain sensitive logic, API keys, or endpoints.

### How to check

**Method 1 — View Page Source**
```
Right-click anywhere on page → View Page Source
(or press Ctrl+U)
```

**What to look for in source code:**

| What you see | Meaning |
|-------------|---------|
| `<script> ... </script>` (no src) | Internal JS — code is right there |
| `<script src="file.js">` | External JS — check the linked file |

### Example source code with External JS:
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>External JS</title>
</head>
<body>
    <h1>Can you verify the JS?</h1>
    <p id="result"></p>

    <!-- Link to the external JS file -->
    <script src="[external-file].js"></script>
</body>
</html>
```

> Seeing `<script src="...">` = External JS The JS logic is inside the linked file, not the HTML

**Method 2 — Browser DevTools**
```
Right-click → Inspect → Sources tab
```
> Shows all JS files loaded by the page

---

# JavaScript — Dialogue Boxes & How Hackers Exploit Them

## Overview

One of JS's main objectives is to provide **dialogue boxes**
for user interaction and to **dynamically update** web page content.

JS provides three built-in dialogue functions:

| Function | Purpose |
|----------|---------|
| `alert` | Display a message to the user |
| `prompt` | Ask the user for input |
| `confirm` | Ask the user for yes/no confirmation |

> **Security Note:** If not implemented securely,attackers can exploit these features to execute **Cross-Site Scripting (XSS)** attacks

> You can test all of these in the **Google Chrome console**
> Right-click → Inspect → Console tab

---

## alert()

### What it does
Displays a message in a dialogue box with an **OK** button.
Typically used to convey information or warnings.

### Syntax
```javascript
alert("message here");
```

### Example
```javascript
alert("Hello THM");
```

**Result:** A popup box appears with "Hello THM" and an OK button

### How to test
1. Open Chrome
2. Right-click → Inspect → Console
3. Type `alert("Hello THM")` and press Enter

---

## prompt()

### What it does
Displays a dialogue box that **asks the user for input**.

| User Action | Return Value |
|-------------|-------------|
| Types something + clicks OK | The entered text |
| Clicks Cancel | `null` |

### Syntax
```javascript
let userInput = prompt("Your question here?");
```

### Example — Ask name and greet user
```javascript
name = prompt("What is your name?");
alert("Hello " + name);
```

**What happens:**
```
1. Dialogue box appears: "What is your name?"
2. User types "Dolo" and clicks OK
3. Alert fires: "Hello Dolo"
```
---

## confirm()

### What it does
Displays a dialogue box with a message and
**two buttons: OK and Cancel**

| User Action | Return Value |
|-------------|-------------|
| Clicks OK | `true` |
| Clicks Cancel | `false` |

### Syntax
```javascript
let result = confirm("Your question here?");
```

### Example
```javascript
confirm("Are you sure?");
confirm("Do you want to proceed?");
```

### Practical usage
```javascript
let answer = confirm("Do you want to delete this file?");
if (answer === true) {
    // delete the file
} else {
    // cancel deletion
}
```

---

## Dialogue Functions Summary

| Function | Returns | Buttons | Use Case |
|----------|---------|---------|----------|
| `alert("msg")` | Nothing | OK | Show info/warning |
| `prompt("msg")` | String or null | OK, Cancel | Get user input |
| `confirm("msg")` | true or false | OK, Cancel | Get yes/no decision |

---

## How Hackers Exploit These Functions

> Imagine receiving an email with an attached HTML file. It looks harmless — but when you open it, it contains malicious JS that disrupts your browsing experience.

### Example — Malicious HTML file (invoice.html)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <title>Hacked</title>
</head>
<body>
    <script>
        for (let i = 0; i < 3; i++) {
            alert("Hacked");
        }
    </script>
</body>
</html>
```

**What happens when victim opens this file:**
```
Loop runs 3 times:
i=0 → alert("Hacked") fires → user must click OK
i=1 → alert("Hacked") fires → user must click OK
i=2 → alert("Hacked") fires → user must click OK
```

> The victim must click OK **3 times** before the page loads
> This is a basic denial-of-experience attack using JS

### Real World Attack Scenarios

| Attack | Method | Impact |
|--------|--------|--------|
| **Phishing** | Send malicious HTML via email | Disrupt/trick victim |
| **XSS** | Inject `alert()` into website | Steal cookies/sessions |
| **Infinite loop** | `while(true) alert("msg")` | Browser crash/freeze |
| **Credential theft** | `prompt()` asking for password | Steal user credentials |

### XSS Example (Cross-Site Scripting)
```javascript
// Attacker injects this into a vulnerable website
<script>alert(document.cookie)</script>

// This steals and displays the victim's session cookies
```

---

# JavaScript — Minification & Obfuscation

## Overview

When pen-testing web applications, you will often encounter
JS code that is **not human-readable**. Understanding
minification and obfuscation is critical for analyzing
what malicious or hidden code is actually doing.

---

## Minification

### What it is
The process of **compressing JS files** by removing all
unnecessary characters without changing functionality.

### What gets removed/shortened
- Spaces and line breaks
- Comments
- Variable names shortened to single letters
- Unnecessary characters

### Why it's used
- **Reduces file size** → faster page loading
- Improves performance in **production environments**
- Code still functions **exactly the same**

```
Original code (readable):          Minified code (compact):
──────────────────────             ────────────────────────
function hi() {          →         function hi(){alert("Welcome to THM");}hi();
    alert("Welcome to THM");
}
hi();
```

---

## Obfuscation

### What it is
The process of making JS code **intentionally hard to
understand** while keeping it fully functional.

### How it's done
- Renaming variables/functions to **meaningless names**
- Adding **dummy/junk code** that does nothing
- Encoding strings in hex or base64
- Wrapping code in complex self-executing functions

### Key Difference from Minification

| | Minification | Obfuscation |
|---|-------------|-------------|
| **Goal** | Reduce file size | Hide code logic |
| **Readable?** | Slightly |  Intentionally not |
| **Functionality** | Same | Same |
| **Used by** | Developers | Developers + Attackers |

---

## Practical Example

### Step 1 — Original readable JS (hello.js)

```javascript
function hi() {
    alert("Welcome to THM");
}
hi();
```

### Step 2 — HTML file linking the JS (hello.html)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <title>Obfuscated JS Code</title>
</head>
<body>
    <h1>Obfuscated JS Code</h1>
    <script src="hello.js"></script>
</body>
</html>
```

### Step 3 — After Obfuscation

The same `hello.js` code after running through an
obfuscation tool becomes:

```javascript
(function(_0x114713,_0x2246f2){var _0x51a830=_0x33bf,_0x4ce60b=_0x114713();
while(!![]){try{var _0x51ecd3=-parseInt(_0x51a830(0x88))/
(-0x1bd3+-0x9a+0x2*0xe37)*(parseInt(_0x51a830(0x94))/
(-0x15c1+-0x2*-0x3b3+0xe5d))+parseInt(_0x51a830(0x8d))/
(0x961*0x1+0x2*0x4cb+0x4bd*-0x4)*...
// continues for many more lines...
'Welcome\x20to','4492Q0mepo',...hi();
```

> This is **the same 4 lines of code** as hello.js! The browser can still execute it perfectly — but humans can barely read it.

---

## Obfuscation in Action — Step by Step

```
Original hello.js                 Obfuscated Output
─────────────────                 ────────────────────
function hi() {        ────►      (function(_0x114713,_0x2246f2)
    alert("Welcome           {var _0x51a830=_0x33bf...
     to THM");               ...gibberish...
}                            ...hi();
hi();
```

**Tools used for obfuscation:**
- [obfuscator.io](https://obfuscator.io/legacy-playground)
- [Code Beautify](https://codebeautify.org/javascript-obfuscator)
- javascript-obfuscator (npm package)
- UglifyJS

---

## Deobfuscating Code

When you find obfuscated JS during a pentest, you need
to **reverse it** to understand what it does.

### Online Deobfuscation Tools

| Tool | URL | Use |
|------|-----|-----|
| **Deobfuscator.io** | [Deobfuscator.io](https://obf-io.deobfuscate.io/) | Undo obfuscator.io output |
| **de4js** | de4js.github.io | General JS deobfuscation |
| **JStillery** | mindedsecurity.github.io/jstillery | Advanced deobfuscation |
| **Prettier** | prettier.io/playground | Beautify/format minified JS |

### Deobfuscation Process

```
Step 1: Copy obfuscated JS code
        ↓
Step 2: Paste into deobfuscation tool
        ↓
Step 3: Click "Deobfuscate"
        ↓
Step 4: Get human-readable code back
```

### Example — Deobfuscated Result

After pasting the obfuscated code into the deobfuscator:

```javascript
function hi() {
    alert("Welcome to THM");
}
hi();
```

> Back to the original readable 4 lines!

---

## Why This Matters for Pentesting

### Attackers use obfuscation to:
- **Hide malicious code** in web pages
- Make malware **harder to detect** by security tools
- Disguise **XSS payloads** in injected scripts
- Conceal **data exfiltration** logic

### As a pentester you need to:

| Situation | Action |
|-----------|--------|
| Find minified JS | Use Prettier to beautify |
| Find obfuscated JS | Use deobfuscation tool |
| Analyze suspicious JS | Look for `eval()`, `document.cookie`, `fetch()` |
| Find external JS file | Download and analyze the `.js` file |

---

# JavaScript — Best Practices & Security

## Overview

When developing or evaluating a web application that uses
JavaScript, following best practices is essential to
**reduce the attack surface** and minimize the chances
of a successful attack.

---

## Avoid Relying on Client-Side Validation Only

### The Problem
JS is commonly used to validate forms on the client side
(in the browser). Many developers **rely entirely** on
this — which is a critical mistake.

### Why it's dangerous
```
User visits website
        ↓
JS validates form input in browser
        ↓
Attacker simply disables JS in browser
        ↓
All validation bypassed! 
```

> A user can easily **disable or manipulate** JS on the client side using browser DevTools

### The Fix
```
Client-side validation  = Good for user experience
Server-side validation  = Essential for security
Both together           = Correct approach
```

> **NEVER** trust client-side validation alone.
> Always **validate again on the server side.**

---

##  Refrain from Adding Untrusted Libraries

### The Problem
JS allows including external scripts using `src`
attribute in a `<script>` tag:

```html
<script src="https://some-library.com/lib.js"></script>
```

### Why it's dangerous
- Bad actors upload **malicious libraries** with names
  that resemble legitimate ones
- If you blindly include a malicious library, you
  **expose your entire web application** to threats
- The malicious library runs with **full JS access**
  to your page, cookies, and user data

### Examples of supply chain attacks
```
Legitimate:   jquery.min.js
Malicious:    jquery.min.js (fake, different CDN)

Legitimate:   bootstrap.js
Malicious:    b00tstrap.js (typosquatting)
```

### The Fix
- Only use libraries from **trusted, verified sources**
- Use **Subresource Integrity (SRI)** hashes to verify
  external scripts haven't been tampered with

```html
<!-- Safe: includes integrity hash -->
<script src="https://cdn.example.com/lib.js"
        integrity="sha384-XXXXXX"
        crossorigin="anonymous">
</script>
```

---

##  Avoid Hardcoded Secrets

### The Problem
Never hardcode sensitive data directly into JS code:

```javascript
//  Bad Practice — NEVER do this
const privateAPIKey = 'pk_TryHackMe-1337';
```

### Why it's dangerous
- JS runs **in the browser** — anyone can view source code
- Attackers can find API keys, tokens, passwords instantly
- `Ctrl+U` or DevTools → Sources reveals everything

### What NOT to hardcode

| Type | Example | Risk |
|------|---------|------|
| **API Keys** | `pk_TryHackMe-1337` | Unauthorized API access |
| **Access Tokens** | `Bearer eyJhbGci...` | Account takeover |
| **Credentials** | `password: "admin123"` | Direct login |
| **Database URLs** | `mongodb://user:pass@host` | Database breach |
| **Secret Keys** | `secretKey: "abc123"` | Crypto/session attacks |

### The Fix
```javascript
// Good Practice
// Store secrets on the SERVER side
// Fetch them via secure API calls
// Never expose them in client-side JS

fetch('/api/get-data', {
    headers: { 'Authorization': 'Bearer ' + sessionToken }
});
// sessionToken comes from server session, not hardcoded
```

---

##  Minify and Obfuscate Your JavaScript Code

### Why it helps
- **Reduces file size** → faster load times
- Makes it **harder for attackers** to understand code logic
- Adds a layer of protection against casual code theft

```javascript
// Original readable code
function calculateTotal(price, tax) {
    return price + (price * tax);
}

// After minification + obfuscation
function _0x3a2f(_0x1b,_0x2c){return _0x1b+(_0x1b*_0x2c);}
```







