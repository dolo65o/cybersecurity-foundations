# Overview 

Burp Suite is an integrated platform for performing security testing of web applications. It includes various tools for scanning, fuzzing, intercepting, and analysing web traffic.
- Java-based framework designed to serve as a comprehensive solution for conducting web application penetration testing.
-  Burp Suite captures and enables manipulation of all the HTTP/HTTPS traffic between a browser and a web server. This fundamental capability forms the backbone of the framework. By intercepting requests, users have the flexibility to route them to various components within the Burp Suite framework

---

# Burp Suite — Key Features

## Core Modules

| Feature | Purpose |
|---------|---------|
| **Proxy** | Intercept & modify requests/responses between browser and web app |
| **Repeater** | Capture, modify and resend requests multiple times — great for SQLi testing |
| **Intruder** | Spray endpoints with requests — used for brute-force & fuzzing |
| **Decoder** | Encode/decode data — transform captured info or craft payloads |
| **Comparer** | Compare two pieces of data at word or byte level |
| **Sequencer** | Assess randomness of tokens like session cookies |

---
# Burp Suite Dashboard Sections

<img width="1132" height="584" alt="The dashboard" src="https://github.com/user-attachments/assets/88e3274e-8646-4f3b-b200-e58ecdba0b75" />


## Tasks
The **Tasks** section manages background activities.  
In **Burp Suite Community**, the default **Live Passive Crawl** automatically logs visited pages and passively analyzes them.  
**Burp Suite Professional** includes advanced tasks like automated scanning.

---

## Event Log
The **Event Log** records actions performed by Burp Suite.

Examples:
- Proxy start/stop
- Connections through proxy
- Errors or warnings

Useful for monitoring and troubleshooting.

---

## Issue Activity (Professional Only)
Shows vulnerabilities found by Burp's automated scanner.

Features:
- Severity levels (High, Medium, Low)
- Confidence level
- Filtering options

Not available in Community Edition.

---

## Advisory
Provides detailed information about vulnerabilities.

Includes:
- Description of issue
- Risk impact
- References (OWASP, CVE)
- Fix recommendations

> Professional version allows exporting reports.
> Community version may not show vulnerabilities.

---

# Burp Proxy 

Burp Proxy allows you to **capture, view, and modify** HTTP/HTTPS traffic between the browser and the target web server.

It is one of the most important tools in **Burp Suite** for testing web applications.

---

## Key Concepts

### Intercepting Requests
When **Intercept is ON**, requests are stopped before reaching the server.

<img width="823" height="437" alt="intercept on" src="https://github.com/user-attachments/assets/6a4a84ab-c7e5-472f-9510-00f293797603" />


You can:
- Forward request
- Modify request
- Drop request
- Send request to other Burp tools

To allow traffic normally:
Turn **Intercept is on → off**

---

### Full Control Over Traffic
Intercepting requests allows testers to:
- Manipulate parameters
- Test input validation
- Check authentication logic
- Modify headers, cookies, tokens

Provides complete control over web communication.

---

### Capture and Logging
Burp automatically logs all traffic passing through the proxy, even when intercept is OFF.

Useful for:
- Reviewing previous requests
- Finding hidden endpoints
- Analyzing application behavior

---

### WebSocket Support
Burp Proxy also captures **WebSocket traffic**, which helps analyze real-time web applications.

Logs available in:
- HTTP history
- WebSockets history

<img width="1111" height="309" alt="HTTP history" src="https://github.com/user-attachments/assets/1ea203f0-1363-40dd-af91-07c3480978d0" />

---

## Proxy Settings

Access using **Proxy → Proxy settings**

Provides control over proxy behavior.

### Response Interception
By default, responses are not intercepted.

Enable:
Intercept responses based on rules

Allows inspecting server responses before they reach the browser.

---

### Match and Replace
Allows automatic modification of requests and responses using regex.

Examples:
- Change User-Agent
- Modify cookies
- Replace headers
- Modify parameters automatically

Useful for repetitive testing scenarios.

---

# Configure Burp Proxy with FoxyProxy (Firefox)

### 1. Install FoxyProxy
Install **FoxyProxy Basic** extension in Firefox.

### 2. Open FoxyProxy Options
Click the **FoxyProxy icon** (top-right corner of Firefox).  
Open **Options**.

### 3. Create New Proxy Configuration
Click **Add** to create new proxy.

Fill details:

| Field | Value |
|------|-------|
| Title | Burp |
| Proxy IP | 127.0.0.1 |
| Port | 8080 |


### 4. Save Configuration
Click **Save**.


### 5. Activate Proxy
Click **FoxyProxy icon** → select **Burp** configuration.

Now browser traffic will pass through:
127.0.0.1:8080

> Burp Suite must be running.


### 6. Enable Intercept in Burp Suite
Go to:

Proxy → Intercept → Turn ON

---

### 7. Test Proxy
Open any website (example target machine).

Browser will pause request.
Request will appear in **Burp Proxy tab**.

You have successfully intercepted traffic.

---

## Important Notes

- When **Intercept ON**, browser requests will stop until forwarded.
- Do not forget to turn intercept OFF after testing.
- Right-click request to:
  - Forward
  - Drop
  - Send to Repeater
  - Send to Intruder
  - Send to other tools

 ---

 # Burp Suite Target Tab 

The **Target tab** helps define testing scope and map the structure of web applications.  
It contains three main sub-tabs.

---

## 1. Site Map

Displays the structure of the target web application in a **tree format**.

Features:
- Automatically records pages visited through the proxy
- Helps understand website structure
- Useful for discovering hidden endpoints
- Captures API endpoints accessed by the application
- Helps during enumeration phase

Burp Professional:
- Supports automated crawling of the website

Burp Community:
- Site map builds as you browse manually

---

## 2. Issue Definitions

Provides a list of common web vulnerabilities detected by Burp Scanner.

Includes:
- Vulnerability descriptions
- Explanation of impact
- References for study
- Helps in writing reports
- Useful for manual testing reference

Available in Community version (without automated scanning).

---

## 3. Scope Settings

Defines which targets Burp will analyze.

Allows:
- Include specific domain or IP
- Exclude unwanted traffic
- Focus testing on selected applications
- Reduce unnecessary data capture

Helps maintain clean and relevant testing environment.

---
# Burp Built-in Browser – Short Notes

Burp Suite provides a **built-in Chromium browser** that is already configured to work with the Burp Proxy.

This removes the need to manually configure proxy settings in Firefox or other browsers.

---

## Start Burp Browser

Steps:
1. Go to **Proxy tab**
2. Click **Open Browser**
3. A Chromium browser will launch
4. All requests from this browser automatically pass through Burp Proxy

---

## Advantages

- No manual proxy configuration needed
- Works instantly with Burp
- Useful for quick testing
- Ensures all traffic is captured automatically

---

## Important Settings

Burp Browser settings can be customized in:

Settings → Tools → Burp's browser

You can modify behavior based on your testing needs.

---

## Issue in Linux (Running as Root)

If running Burp as **root user**, the browser may not start due to sandbox restrictions.

### Solutions

### Smart Option
Create a normal (low-privilege) user and run Burp Suite from that account.

More secure approach.

---

### Easy Option
Go to:

Settings → Tools → Burp's browser

Enable:
Allow Burp's browser to run without a sandbox

This allows the browser to start.

Warning:
Disabling sandbox reduces security.
If browser is compromised, attacker could access system.

---

# Burp Suite Scoping – Short Notes

**Scoping** helps limit Burp Suite to capture and log only the traffic related to the target web application.

Without scope, Burp logs all browser traffic, which creates unnecessary noise.

---

## Why Scoping is Important

- Focus only on target application
- Avoid capturing irrelevant traffic
- Makes analysis easier
- Keeps HTTP history clean
- Improves testing efficiency

---

## Add Target to Scope

![Add scope through target](https://github.com/user-attachments/assets/5b6a54fc-cddf-4330-aef1-12381b9fc2e9)


Steps:
1. Go to **Target tab**
2. Select target from left panel
3. Right-click → **Add to scope**
4. Choose **Yes** to stop logging out-of-scope traffic

Burp will now prioritize selected target only.

---

## View or Edit Scope

Go to:

Target → Scope settings

You can:
- Include specific domains/IPs
- Exclude unwanted targets
- Control which traffic is recorded

---

## Restrict Proxy to Scope Only

Even after setting scope, Burp may still intercept all traffic.

<img width="1265" height="811" alt="Intercept Client Requests" src="https://github.com/user-attachments/assets/fe08aa2c-d5f1-44dc-b966-9b69045a3d3e" />


To fix:

1. Go to **Proxy tab**
2. Open **Proxy settings**
3. Find **Intercept Client Requests**
4. Enable:

And URL Is in target scope

Now Burp will ignore out-of-scope traffic completely.

---

