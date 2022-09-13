# SQL statements summary

At a high level, SQL syntax has the following main categories: statements, clauses, expressions, keywords and identifiers.

The fundamental unit of SQL is **SQL statement**, also known as **SQL command**. The distinction is unclear and it seems that these notions are used interchangeably, and hence are synonymous. What is worse, sometimes "SQL query" is used to mean "SQL statement". Here, we reserve **SQL query** to mean specifically SELECT statements (see below). An SQL statement is the smallest complete piece of SQL code that can be executed independently and it usually results in the permanent change of state of an object in the database, e.g., schema, table, user, etc. As such, SQL statements either return nothing, or return record sets (in the case of the SELECT statement). In contrast, an **SQL expression** is a minimal syntactically correct executable piece of code. Unlike statements, expressions return a typed value (i.e., not a record set), such as integers, booleans, strings, etc., and they don't change the state of the database objects on their own. A **clause** is a section of a statement, that modifies its control flow, or adds additional constrains to the statement. Some clauses are optional for some statements and others are mandatory, in particular, every statement must have at least one clause. **Keywords** are used to designate different clauses and **identifiers** are used to refer to named entities, such as tables, macros, functions, etc. Thus, roughly, SQL code consists of a series of statements, that are composed of one or more clauses, which are introduced with their specific keywords and contain expressions and identifiers. A statement must terminate with a semicolon (';') symbol.

SQL commands can subdivided into several categories as follows.

### Data Definition Language (DDL) commands

The DDL family of commands includes commands that alter the structure of the database itself, e.g., by creating or deleting tables, altering schemas, etc.

- CREATE creates

### Data Manipulation Language (DML) commands

The DML family of commands contains commands that manipulate records in the database, e.g., inserting, updating or deleting sets of rows from the tables.

### Data Control Language (DCL) commands

The DCL family of commands includes commands to set access permissions for different objects in the database. They are used to grant and revoke permissions to database users.

### Transaction Control Language (TCL) commands

The TCL 