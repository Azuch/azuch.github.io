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

- [column] LIKE : %: any characters; _: 1 character.
- BETWEEN int AND int
- AND
- OR
- <, >, =

## II. Advanced:

### 1. Join

- SELECT FROM [table1] [option] JOIN [table2] ON [table1.id_to_ref] = [table2_id_to_ref]: It join using the FORGREIN KEY, which is set for 2 tables, like: bands.id = albums.band_id

TABLE1 | TABLE2
LEFT   | RIGHT

[option]
- INNER: Default, show only matches.
- RIGHT: Show all of the second table 
- LEFT: Show all of the first table.

### 2. Aggregate

- SELECT [Aggregate_function]([DISTINCT] colum) FROM [table]

- [Aggregate_function]: SUM, MIN, MAX, COUNT...

### 3. Aggregate and Group By

- Aggregate is use on group only, when no group is selected, the whole table is a group.
- When using group by, the aggregate will iterate on first group, the the second...
- The Aggerate is execute after the group by, so it can not be used with the WHERE, which is before the group by.
- Instead, we using the HAVING

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
