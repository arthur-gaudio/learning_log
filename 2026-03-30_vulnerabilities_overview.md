# Daily Log — Path Traversal, Access Control, and Authentication Basics
- Date: 2026-03-30  
- Time spent: 3 hours  
- Focus: Studied PortSwigger apprentice topics on path traversal, access control, and authentication vulnerabilities

---

## 1) What I learned (high level)
- Path traversal vulnerabilities can allow attackers to access arbitrary files on the server by manipulating file path input.
- Access control issues happen when users can reach data or functionality they should not be allowed to access, including vertical and horizontal privilege escalation.
- Authentication flaws can expose login systems to brute-force attacks, username enumeration, and weak two-factor authentication flows.

---

## 2) Key concepts / notes
### 2.1 Path traversal and access control
- Path traversal (directory traversal) happens when user input is used to build file paths unsafely, which can allow reading sensitive files outside the intended directory.
- Reading arbitrary files through path traversal can expose configuration files, credentials, or application data.
- Access control is about enforcing what a user is allowed to do after they are authenticated.
- Vertical privilege escalation means a user gains access to functionality reserved for higher-privileged users, such as admin features.
- Horizontal privilege escalation means a user accesses another user’s data or actions at the same privilege level.
- Parameter-based access control is risky when the application trusts values in the request, such as role IDs, user IDs, or hidden parameters.
- Unprotected functionality and unpredictable URLs are not real security controls if authorization checks are missing on the server side.

### 2.2 Authentication vulnerabilities
- Authentication verifies who a user is, while authorization decides what that user is allowed to access.
- Brute-force attacks target login mechanisms by trying many username/password combinations.
- Username enumeration happens when an application reveals whether a username exists through different responses, errors, or timing behavior.
- Weak authentication logic can make brute-force attacks easier if the system lacks proper rate limits, lockouts, or consistent responses.
- Two-factor authentication can still be bypassed if the implementation does not properly enforce the second verification step.
- Secure authentication design depends on:
  - consistent error messages
  - rate limiting / lockout protections
  - strong session handling
  - correctly enforced multi-factor logic

---

## 3) Code snippets
```
# No code today
```

## 4) Exercises completed
Exercises completed in the Portswigger learning path

### What I struggled with:
- Keeping the difference between authentication and authorization clear at first when moving through the topics quickly.
- Thinking through how horizontal and vertical privilege escalation differ in real request flows.

### What clicked:
- Access control issues are often simple logic failures on the server side, not just “hidden links” or UI mistakes.
- Parameter-based access control is dangerous when the application trusts request values without validating permissions server-side.
- Authentication and authorization are separate problems, and both need to be enforced correctly for security to hold.

## 5) Output shipped today
- Notes committed

## 6) Tomorrow plan (specific)
- Continue with the PortSwigger learning path
