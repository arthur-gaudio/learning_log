# Daily Log — SQL Injection Intro + OWASP Injection Reading
Date: 2026-03-23 
- Time spent: 2 hours  
Focus: Studied the introduction to SQL injection in PortSwigger and read the OWASP Top 10 Injection topic

---

## 1) What I learned (high level)
- SQL injection happens when untrusted input is interpreted as part of a backend SQL query.
- Basic SQL injection impact includes retrieving hidden data, changing application logic, and expanding access to data that should not be exposed.
- UNION-based SQL injection is a key technique for combining attacker-controlled query results with the original query output.
- OWASP Injection covers more than just SQL injection and emphasizes that unsafe handling of untrusted input can lead to serious security risks.
- Prevention is centered around secure coding practices such as parameterized queries and separating data from commands.

---

## 2) Key concepts / notes

### 2.1 SQL injection fundamentals
- SQL injection happens when application input is inserted into a SQL query in an unsafe way.
- A vulnerable application may allow an attacker to:
  - retrieve hidden data
  - bypass intended filtering
  - change application behavior
  - sometimes interact with the database in unintended ways
- Today’s PortSwigger progress covered:
  - What is SQL injection?
  - How to detect SQL injection vulnerabilities
  - Retrieving hidden data
  - Subverting application logic
  - SQL injection UNION attacks
  - Determining the number of columns required

### 2.2 Detection and exploitation concepts
- Detecting SQL injection often starts with observing how the application responds when input is slightly changed.
- UNION attacks depend on matching the structure of the original query, including the number of columns.
- Determining the number of columns is an important step before extracting useful data through UNION-based attacks.
- The application response can reveal useful clues such as:
  - different output behavior
  - errors
  - changes in returned content
  - successful rendering of injected results

### 2.3 OWASP Injection notes
- Injection is still a major web application security risk because untrusted input can be interpreted as commands or queries.
- The root issue is treating user-controlled input as code/logic instead of data.
- Main prevention ideas:
  - use parameterized queries / prepared statements
  - validate and constrain input
  - avoid building queries through string concatenation
  - apply least privilege to database accounts
  - handle errors securely so sensitive internals are not exposed
---

## 3) Code snippets (if any)

```python
# No Python code today
```

## 4) Exercises completed
- Completed in the Learning Path
- Very basic labs to understand the topic

### What I struggled with:
- Getting comfortable with writing parts of queries in fields and parameters I am not used to.
- Keeping the UNION attack logic straight in my head, especially why the number of columns has to match.
- Understanding how application behavior changes can hint at a successful SQL injection attempt even before full data extraction.

### What clicked:
- The big picture of SQL injection: user input becomes dangerous when it changes the meaning of the backend query.
- Why determining the number of columns matters before using UNION.
- The connection between PortSwigger lab topics and OWASP’s broader explanation of Injection and prevention.

## 5) Output shipped today
 - Notes committed

## 6) Tomorrow plan
- Continue SQLi Path in PortSwigger
