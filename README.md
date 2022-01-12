# COSC 404 - Database System Implementation<br/>Lab 3 - Implementing a Text Database and JDBC Driver

This lab practices programming with a JDBC driver.

## Your Own Text Database with a JDBC API (30 marks)

In this question, we will build our own text database stored as a text file.  A single record is stored on one line. The fields in each record are separated by tabs
("\t" in Java Strings). The source code consists of some junit tests and the code files in package `textdb`.  The application also has a functioning text menu that prompts and reads in information for the methods to implement. All marking will be based on successfully completing the `junit` tests.  [Sample output](output.txt) is also available.

The first step is to complete the `TableHandler.java` file that performs the actual methods for search, insert, delete, and update.  Below is the marking for these methods:

- `readAll()` - to read and print out all records (2 marks)
- `findRecord(String key)` - to find a specific record with the specified key and output the record (5 marks)
- `findStartOfRecord(String key)` - may be helpful to find a specific record and return the byte offset into the file of this record from the start of the file (marks are included with findRecord)
- `insertRecord(String record)` - to add a new record to the text file in the proper format (2 marks)
- `deleteRecord(String key)` - to find a specific record with the specified key and remove the record from the text file (3 marks)
- `updateRecord(String key, int col, String value) - to locate record with key and update the specified column with the new value. (6 marks)

Note that deletes and updates are **EXTREMELY** inefficient as they require re-writing anything in the file after the insertion or deletion point.  This is acceptable for an answer, and you do not need to try to come up with anything more efficient.  However, it should motivate why we store tables in blocks and records in a database for much better performance.

The second component of the assignment is to make a simple JDBC driver for your text database.  Most of the key classes have already been created and default methods produced.  You are only responsible for modifying these methods:

- `TextDBStatement.executeQuery()` - should execute a SELECT style query.  Can be either `SELECT ALL` (read all records) or `SELECT <i>key</i>` (e.g. `SELECT 5`) which would return record with key 5.  (2 marks)
- `TextDBStatement.executeUpdate()` - should execute these commands: (2 marks)
	- `DELETE <i>key</i>` (e.g. `DELETE 5`)
	- `INSERT *record*` (e.g. `INSERT 33	Lawrence	44	9`).  Note that the fields are already tab-delimited to make it easier to do the insert (can write the record directly to the file by calling appropriate method in TableHandler).
	- `UPDATE *key column value*` (e.g. `UPDATE 2	2	Change Special Company Export`).  Note that fields are also tab separated for convenience.
- `TextDBResultSet.TextDBResultSet()` - constructor to setup ResultSet (2 marks)
- `TextDBResultSet.next()` - `next()` method advances to next output row in ResultSet (2 marks)
- `TextDBResultSet.getObject()` (both column number and column name versions).  Returns either an Integer or String object depending on if data is int or String.

**2 marks of the 30 are awarded based on comments and code style/indenting.**  The TA will assign marks as follows:

- 0 - code has no comments and is hard to read
- 1 - code has some comments, is mostly indented, and has a readable style
- 2 - code demonstrates professional quality comments and style
