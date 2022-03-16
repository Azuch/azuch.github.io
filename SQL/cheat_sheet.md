# Here are something to reference to SQL.

## I. Basic foundation

*Before do anything, you must select database: USE [database]

- PRIMARY KEY ([id_column]): The unique id for individual record of individual table.
- FORGREIN KEY ([id_to_ref]) reference [table_dest] ([id_dest]): Reference to another id of foregein table.
- CREATE DATABASE [db_name]
- CREATE TABLE [tb_name] ([col1_name] [type], [col2_name] [type]...)
- SELECT DISTINCT [column] FROM [table]: Show unique to all duplicate
- INSERT INTO [table] ([col1], [col2]...) VALUES ([val1], [val2]...)
- UPDATE [table] SET [column = [value]] WHERE [coolumn meets condition]: Update the value of the column of the table, which meets the condition(s).
- DELETE FROM [table] WHERE [column meets condition(s)]

- [column] LIKE '%Alex%': same same.
- BETWEEN int AND int
- AND
- OR
- <, >, =

## II. Advanced:

- Join

## III. The Cheat Sheet
<details><summary>Part one</summary>

![This is an image](./SQL-cheat-sheet_page-0002.jpg)

</details>

<details><summary>Part two</summary>

![This is an image](./SQL-cheat-sheet_page-0001.jpg)

</details>

<details><summary>Part three</summary>

![This is an image](./SQL-cheat-sheet_page-0003.jpg)

</details>


***Thanks sqltutorial.com***
