# Daily Log — SQL Injection Topic Completed
- Date: 2026-03-28  
- Time spent: 3 hours  
- Focus: Finished the full SQL injection topic in PortSwigger and consolidated my understanding of the main SQLi techniques and prevention methods

---

## 1) What I learned (high level)
- SQL injection has many forms beyond the basic examples, including UNION-based, blind, error-based, time-based, out-of-band, second-order, and context-specific attacks.
- Blind SQL injection requires paying close attention to indirect application behavior, such as conditional responses, timing differences, and external interactions.
- Prevention is just as important as exploitation knowledge, especially parameterized queries, safe query construction, least privilege, and secure error handling.

---

## 2) Key concepts / notes
### 2.1 SQL injection attack patterns
- UNION attacks depend on matching the structure of the original query, including the correct number of columns and compatible data types.
- Retrieving interesting data often requires understanding which columns can display useful output.
- Multiple values can sometimes be combined into a single column for extraction when output space is limited.
- Database enumeration helps identify the structure of tables, columns, and the environment before attempting further extraction.

### 2.2 Blind, advanced, and defensive understanding
- Blind SQL injection relies on indirect signals instead of visible query output.
- Conditional-response SQLi uses changes in application behavior to infer true/false conditions.
- Error-based SQLi uses database error messages or behaviors to reveal useful information.
- Time-delay SQLi uses response timing to infer whether payload logic succeeded.
- OAST-based SQLi uses out-of-band interactions when the application does not return useful direct output.
- Second-order SQL injection happens when stored input becomes dangerous later in a different query context.
- Prevention includes:
  - parameterized queries / prepared statements
  - avoiding dynamic query concatenation
  - least-privilege database accounts
  - safe error handling
  - secure input handling

---

## 3) Code snippets (if any)
```SQL
-- Example SQLi concept note: UNION-based extraction
SELECT name, description
FROM products
WHERE category = 'Gifts'
UNION
SELECT username, password
FROM users;
```

---

## 4) Exercises completed

Exercises completed in PortSwigger itself during study - labs included in the SQLi Learning path.

### What I struggled with:
- Keeping the different blind SQL injection techniques clearly separated in my head at first, especially conditional responses vs time delays vs OAST.
- Understanding how second-order SQL injection differs from direct input-based SQL injection.

### What clicked:
- SQL injection is not just one technique; it is a family of attack patterns depending on how the application handles input and output.
- Blind SQL injection became much clearer once I focused on indirect signals instead of expecting visible query results.
- Prevention makes more sense now because I can connect each control to the specific weakness it is meant to stop.

---

## 5) Output shipped today
Notes committed

---

## 6) Tomorrow plan
- Do more SQLi labs to solidify my understanding
- Choose the next vulnerability topic to study
