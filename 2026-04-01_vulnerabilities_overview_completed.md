# Daily Log — SSRF, File Upload Vulnerabilities, and OS Command Injection
Date: 2026-04-01  
Time spent: 2 hours  
Focus: Studied PortSwigger apprentice topics on server-side request forgery (SSRF), file upload vulnerabilities, and OS command injection

---

## 1) What I learned (high level)
- SSRF happens when a server fetches attacker-controlled URLs and can be abused to access internal services or unintended back-end systems.
- File upload vulnerabilities can lead to serious impact when validation is weak, including web shell upload and remote code execution.
- OS command injection occurs when untrusted input is passed into operating system commands, allowing attackers to execute commands on the server.

---

## 2) Key concepts / notes
### 2.1 SSRF and file upload vulnerabilities
- SSRF allows an attacker to make the server send requests on their behalf, which can expose internal-only systems and services.
- Basic SSRF attacks can target:
  - the application server itself
  - local services
  - other back-end systems on the internal network
- SSRF is dangerous because the server may have more trust and network access than an external attacker.
- File upload vulnerabilities happen when the application does not properly restrict what files can be uploaded.
- Weak validation can allow:
  - dangerous file types
  - content-type bypasses
  - files that execute as code on the server
- Web shell upload is especially severe because it can lead directly to remote code execution and deeper server compromise.
- File upload defenses need to validate more than just the extension or Content-Type header.

### 2.2 OS command injection
- OS command injection happens when user input is inserted into a system command unsafely.
- If the server executes the input as part of a shell command, an attacker may run arbitrary commands on the host.
- Even simple command injection can expose:
  - system files
  - environment details
  - application data
- OS command injection often has very high impact because it can lead to full server compromise.
- Safe design depends on:
  - avoiding shell execution when possible
  - separating input from commands
  - strict validation
  - least privilege for the running process

---

## 3) Code snippets
```
# No code today
```
---

## 4) Exercises completed
Exercises completed in the Portswigger learning path

### What I struggled with:
- Thinking through SSRF from the server’s point of view instead of the attacker’s browser point of view.
- Keeping the file upload attack paths separate in my head, especially extension checks vs content-type checks vs execution on the server.

### What clicked:
- SSRF makes more sense when I think of it as “abusing the server’s network trust.”
- File upload vulnerabilities are dangerous because weak validation can turn a normal feature into code execution.
- OS command injection is conceptually similar to other injection flaws: user input changes the meaning of what the server executes.

---

## 5) Output shipped today
Notes committed

---

## 6) Tomorrow plan
- Continue with the next PortSwigger topics
