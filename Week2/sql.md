## SQL

**SQL is a relational database language**

You may hear different implementation of a SQL database such as Oracle, PostgreSQL, MySQL. These differ in advanced functionality the basics and language specifics are the same:

###What makes up a SQL database?

One database can have many many tables. Each table has columns and rows.

Each new item inserted into a table occupies a new row. 

When you define a table, you define columns that represent fields of the data.

For example:

STUDENT_TABLE

| NAME | GPA | YEAR | ADVISOR |
|------|-----|------|---------|
| Bob  | 3.2 | 2018 | Smith   |
| Jill | 3.3 | 2019 | Jones   |

This table has two data points, the students Bob and Jill and we know their name, gpa, year and advisor.

###Creating SQL Table:
 
Basic syntax:
```SQL
CREATE tableName (columnName columndataType, columnName columnDataType);
```
Example:
```SQL
CREATE GROCERY_TABLE (_ID INTEGER PRIMARY KEY, GROCERY_NAME TEXT);
```

###Adding data to a table

When you are creating a SQL table you can specify NON NULL after column data type to require that column must be specified on the request.
There are a ton of wrappers around pure SQL that make it so you don’t have to type out strings to insert into the database.
However the string to do so would look like:
```SQL
INSERT INTO GROCERY_TABLE (GROCERY_NAME) VALUES (“EGGS”);
```
 
In Android there is a nice wrapper so inserting into a database will look like this:

```java
public boolean writeToDatabase(String groceryItem, int position) {
	    ContentValues insertValues = new ContentValues();
        insertValues.put(GrocerySchema.GROCERY_ITEM_COLUMN, groceryItem);
        insertValues.put(GrocerySchema.POSITION_COLUMN, position);
    	try {
            writableGroceryDb.insertOrThrow(GrocerySchema.TABLE_NAME, null, insertValues);
        	return true;
    	} catch (Exception ex) {
            Log.e("Database Service", "Error occurred inserting into database", ex);
        	return false;
    	}
	}
```
	
####Explaining this code:
ContentValues is a specific implementation of a map where you put column names as keys and values as values

```Java 
writableGroceryDb.insertOrThrow(GrocerySchema.TABLE_NAME, null, insertValues);
```
In that line I simply specify the table I wish to insert into and the values I wish to insert in and I can write data to a database
This method will throw a SQLException if I did something wrong like specify an incorrect column name, but otherwise it should work splendidly
 
###Reading from a table:
There are two main components to reading from a SQL table, the column selection and the selection clause.

A Read command in SQL could look like this:

```
Select GROCERY_NAME FROM GROCERY_TABLE; 
```
-Select the GROCERY_NAME of all rows in the table

```
SELECT GROCERY_NAME FROM GROCERY_TABLE WHERE _ID = 5;
```

select the GROCERY NAME of all Rows where _ID = 5

```
SELECT * FROM GROCERY TABLE;
```

get everything from GROCERY_TABLE

####Android Implementation:

            String[] columnsToQuery = {
                    GrocerySchema.GROCERY_ITEM_COLUMN,
                    GrocerySchema._ID
            };
            Cursor groceryCursor = readableGroceryDb.query(GrocerySchema.TABLE_NAME, columnsToQuery , null, null, null, null ,null);

http://developer.android.com/reference/android/database/sqlite/SQLiteDatabase.html

Shows you more about the query method and why so many parameters are null.

However, the code I have written queries all rows from the table defined with GrocerySchema.TABLE_NAME

####Cursor
You have to use the cursor to add your data into an ArrayList.

Imagine a cursor is is essentially a tool that is pointing at the results you got. It points at one particular row and if we want to look at a different row we would have to call something like
```
groceryCursor.next();
```
However, before we get any data from it we need to move it to be looking at the first row or it is initialized into this really odd state of pointing at nothing. to do that use the method
```
groceryCursor.moveToFirst();
```

```
groceryCursor.getString(0)
```
 This will get the string from the row we are presently pointing at that is at column 0.

In the sample code above we would get be looking at data that looks something like this table below

| GROCERY_ITEM_COLUMN | _ID |
|------|-----|
| Eggs  | 1 |
| Bacon | 2 |


Calling getString(0) will return the GROCERY_ITEM_COLUMN

###Deleting Data

Deleting follow a pattern very similar to reading, in that you need to specify a WHERE clause to determine what to delete
```
DELETE FROM GROCERY_TABLE WHERE _ID = 5;
```
In Android there is a method very similar to query() called delete() that will delete data


