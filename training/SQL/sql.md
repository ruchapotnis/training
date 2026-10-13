---
layout: default
title: AWS Training
---


# Why SQL?

Businesses keep track of their data in databases. **SQL analyses data from this database and generates valuable insights** by us writing a query. 

For example, a person can get information about a button on a website, such as:
* How many times users are clicking on that particular button.
* This data is stored in the database. 
* If it's a lot, maybe changing the placement of that button to make it more visible to the users as user interaction can be more.

How would one get this information that many people are using this particular button? **With the help of SQL.** 

SQL helps to get that data. All data consists of hidden insights. With the help of SQL, we can unlock those hidden values. SQL helps to retrieve data from databases.

# What is SQL?

**SQL** stands for **Structured Query Language**. It is a standardized programming language used to interact with databases. With SQL, you can:
* **Retrieve** data
* **Filter** data
* **Add** new data
* **Update** existing data
* **Remove** data from a database

## Understanding Databases and RDBMS

A **database** is a organized collection of tables that share specific relationships with one another. 

To manage these databases, we use a **Relational Database Management System (RDBMS)**. Common examples of an RDBMS include:
* **Oracle**
* **Microsoft SQL Server**
* **MySQL**

## Environment Setup: Microsoft SQL Server & SSMS

For this guide, we use **Microsoft SQL Server** because most of its core components are available for free (specifically the Developer version using the Basic setup option).

To interact with the server, you must install a graphical frontend tool called **SQL Server Management Studio (SSMS)**. This is where you write queries and manage your database objects. 

### Connection Workflow
1. **Launch** SSMS.
2. **Connect** SSMS to your local or remote Microsoft SQL Server instance.
3. **Access** the SQL Server management view to start writing queries.

## Relational Databases & Normalization

Databases are broken down into smaller, simpler tables to maintain organization. These tables correlate with one another using unique identifiers known as **IDs**. Because of these core connections, they are known as **relational databases**.

When designing a database structure, the primary goal is to minimize data redundancy. The structured process of reducing data repetition across tables is called **normalization**.

## Executing Queries

When working inside the query editor interface:
* The **SQL query** window is located at the top.
* The corresponding **results pane** populates directly at the bottom. 
* A standard initial execution window often fetches a large data set (e.g., a result set of **1000 rows**).

![Alt text](./images/image1.png)

## Table Components
The results section of a database query is structured like a regular data table:
* **Fields:** The columns of the table that define the categories of data.
* **Records:** The rows of the table that represent individual entries.

## Data Granularization
To query against data effectively, it must be simplified and broken down to its most granular level. For example, location data is split into distinct fields rather than being combined into a single text block:
* City
* State
* Country
* Zip Code

Breaking data down this way makes it much easier to filter, sort, and query.

## Connecting Tables
Databases store information across multiple separate tables. A connection can be established between any two tables whenever they share **something in common** (such as a matching ID or key field).

![Alt text](./images/image2.png)

- Both the tables have ‘Customer ID’ in common. Hence both the tables are related with the help of ‘Customer ID’.
- Customer ID in the first table (customer table) also happens to be the primary key. Primary key is the minimum number of columns you need to uniquely identify a record. It helps us to uniquely identify a row or a column (records). In the second table (order table), the unique identifier is the Order ID hence it is the primary key. 
- Database diagram is also present. We can also create our own database diagram.

![Alt text](./images/image3.png)


- Database diagram shows the databases which are present along with their fields. The small yellow in each database is the primary key (unique identifier) in each database. 
- In the order product table, there is no individual primary key. In that table to uniquely identify an item it is the Order ID and the cookie ID. 
- For many different customers, there can be many orders. Hence outside the table there is an infinity sign indicating one to many relationships. Similarly, for each orders there are many order products. Lastly, for one product there can be many order products as well. 
- We can also get an idea of the data type of each table. During querying, it becomes easier.


# QUERY

1. We want see all the list of customers. When we look at the customer database, there is one called ‘customerName’.

![Alt text](./images/image4.png)

1. **Start with SELECT:** The `SELECT` command allows us to retrieve data from a table. 
2. **Specify the column:** Type `CustomerName` exactly as it is mentioned in the database schema.
3. **Indicate the source:** Next, we need to mention where we want to get the customer name from—hence, type `FROM`. 
4. **Name the table:** It is obtained from the `dbo.Customers` database, so type `dbo.Customers`.
5. **Run the query:** Click on **Execute** to see your results.

#### 💻 Complete Query Example
```sql
SELECT CustomerName 
FROM dbo.Customers;
```

2. To include the specific notes associated with each customer in your current reporting or database query, update your existing selection block to append the `Notes` field. 

### Implementation
Keep the rest of your original query structure exactly the same, and modify your target fields list as shown below:


![Alt text](./images/image5.png)

```sql
/* Update your SELECT statement by appending the notes column */
SELECT CustomerID, CustomerName, ContactEmail, Notes
FROM Customers;
```

* **Adjustment:** Just add `Notes` with a comma following your preceding field. 
* **Consistency:** The remaining filters, joins, and sorting parameters of the query do not need to change.

3. ## Working with Multiple Databases
* **Simultaneous Connections:** SQL environments allow you to connect to and work with multiple databases at the same time.
* **Context Selection:** The active database context is typically visible in the connection settings (e.g., a dropdown menu located at the top-left of the application interface showing a specific database like `KCC`).

## Preventing Context Failures (The Master Database Issue)
* **Execution Errors:** If your current session context is set to a system database like `master`, executing a query against local tables (e.g., `dbo.customers`) will fail. 
* **Cause:** The table `dbo.customers` does not exist inside the system `master` schema.

![Alt text](./images/image6.png)

## Multi-Database Referencing Solution
* **Explicit Naming:** You can query tables outside your active database context by using a fully qualified domain reference.
* **Syntax Pattern:** Prepend the target database name directly before the schema and table name using standard dot notation.
* **Implementation Example:** Change your standard table call to a fully qualified target reference:
  ```sql
  -- Standard query (fails if active context is not 'KCC')
  SELECT * FROM dbo.customers;

  -- Fully qualified query (succeeds regardless of active context)
  SELECT * FROM KCC.dbo.customers;
  ```


4. ## The Formatting Challenge
When querying columns from a relational database, column identifiers frequently use formatting variants like PascalCase (e.g., `CustomerName`) or underscores to maintain backend naming standards. However, these raw identifiers often lack user-friendly formatting when displayed directly on reporting dashboards or customer-facing outputs.

![Alt text](./images/image7.png)

## The Solution: Column Aliasing
To insert a blank space or create a readable name for a column header, utilize the **`AS` keyword** followed by an identifier enclosed in square brackets (`[...]`). 

### Key Syntax Rules
* **The `AS` Keyword:** Appended immediately after the target database column name to indicate a temporary rename in the output.
* **Square Brackets (`[]`):** Function as explicit delimiters in relational database dialects (such as SQL Server). They instruct the query engine to interpret any characters enclosed within them—including whitespace—as a single literal string identifier rather than system keywords or separate syntax commands.
* **Flexibility:** Any custom title can be added inside the brackets to meet your specific structural presentation or business requirements.

### Implementation Comparison

| Before Aliasing | After Aliasing |
| :--- | :--- |
| Returns standard unspaced table header. | Returns structured column header with spaces. |
| `SELECT CustomerName FROM dbo.customers;` | `SELECT CustomerName AS [Customer Name] FROM dbo.customers;` |


5. # SQL: Obtaining Distinct and Unique Records

## The Problem: Duplicate Rows in Query Results
When querying tables with repeated data—such as a customer list where a company like **Tres Delicious** appears multiple times because it has different headquarters or branch offices—a standard `SELECT` statement returns every matching row. This leads to duplicate entries in your final result set.

![Alt text](./images/image8.png)

## The Solution: The `DISTINCT` Keyword
To filter out duplicate rows and return only unique values, insert the **`DISTINCT`** keyword immediately after the `SELECT` command.

### Syntax Implementation
```sql
SELECT DISTINCT CustomerName
FROM KCC.dbo.customers;
```

### How It Works
1. **Scans the Columns:** The database engine evaluates the combination of columns specified after the `DISTINCT` keyword.
2. **Eliminates Redundancy:** If a value like *Tres Delicious* occurs more than once in the target column, the engine removes the duplicates from the output display.
3. **Consolidated Output:** The final result list displays each unique customer name exactly **once**, regardless of how many times it exists inside the underlying database table.

6. ## 6. Retrieving All Columns in SQL

To retrieve all columns and records from a specific table in a database, use the **`SELECT *`** statement. The asterisk (`*`) acts as a wildcard that tells the database engine to return every column available in that table.

### Basic Syntax
```sql
SELECT * FROM table_name;
```

![Alt text](./images/image9.png)

### How It Works

* **`SELECT`**: The primary clause used to query data from a database.
* **`*`**: The wildcard character specifying that **all columns** should be included in the results.
* **`FROM table_name`**: Specifies the exact table where the data is located.

## 7.  Retrieving Top 3 Columns in SQL

### Basic Syntax
```sql
SELECT top(3) * FROM table_name;
```

![Alt text](./images/image10.png)


## 8. Filtering with WHERE

To retrieve the list of customers in the state of WA
### Basic Syntax
```sql
SELECT * FROM table_name 
where State = 'WA';
```

* Feel free to insert spaces to make it look cleaner and better.
* Entering comments also help with the help of **`--`** or **`/*`**

![Alt text](./images/image11.png)

In the above example, we filtered data equal to `WA` state. 
We can also filter data `not equal` to WA state using `!=` or `<>`

![Alt text](./images/image12.png)


## 9. Using OR statement

We can also filter the data with multiple states. For e.g. if we want two states, we use `OR`

![Alt text](./images/image13.png)


## 10. Using IN and NOT IN

![Alt text](./images/image14.png)

![Alt text](./images/image15.png)


## 11. Using AND

We can type a query where we specifically want a customer with a specific country. For that we type `AND`

![Alt text](./images/image16.png)


## 12. Combining AND with OR Operators

To search for a customer in a specific country who matches one of multiple criteria, combine `AND` with `OR` using parentheses `()`.

**Syntax Example:**
```text
Country = 'USA' AND (Status = 'Active' OR Lifetime_Value > 1000)
```

**How it works:**
* The system first evaluates the conditions inside the **parentheses** (`Status` or `Lifetime_Value`).
* It then ensures the customer *must* also match the **Country** requirement.


![Alt text](./images/image17.png)


## 13. Filtering with the `LIKE` Operator

To find customers whose names begin with the letter **A**, use the `LIKE` operator combined with the `%` wildcard. The `%` sign implies that there can be any character (or no characters) after the letter **A**, as long as the value begins with **A**.

![Alt text](./images/image18.png)

**Example Query:**
```sql
SELECT * FROM table_name 
WHERE customer_name LIKE 'A%';
```

**Key Details:**
* **Result**: This query returns the **two customers** whose names begin with the letter **A**.
* **The `%` Wildcard**: Ensures that only the starting letter is restricted to **A**, allowing any sequence of letters to follow it.


![Alt text](./images/image19.png)

To find customers whose names do **not** start with the letter **A**, use the `NOT LIKE` operator. This explicitly reverses the filter and excludes any matching patterns.

**Example Query:**
```sql
SELECT * FROM table_name
WHERE customer_name NOT LIKE 'A%';
```

**Key Details:**
* **Result**: This query filters out the customers starting with **A** and returns all other customer records.
* **The `NOT` Modifier**: Prepending `LIKE` with `NOT` instructs the system to look for a complete lack of a match against the `'A%'` pattern.


## 14. Filtering with the `WHERE`

To filter rows based on specific numeric ranges or boundaries, use the `WHERE` clause combined with comparison operators. For example, you can filter for records where the order total is greater than 1000.

![Alt text](./images/image20.png)

**Example Query:**
```sql
SELECT * FROM orders 
WHERE order_total > 1000;
```

**Key Operators:**
* **Comparison Operators**: You can use `>=` (greater than or equal to), `<=` (less than or equal to), `<` (less than), or `=` (equal to) to fine-tune your limits.
* **The `BETWEEN` Operator**: To filter within an inclusive range, use `BETWEEN`. For example, `WHERE order_total BETWEEN 1000 AND 5000` catches all 


![Alt text](./images/image21.png)

# Joining Two Tables

This will be inclusive of 1000 and 2000.

It is very important to join two tables. In the above queries, we were just pulling information from one table. Now we are going to pull information from two tables and get results as one spreadsheet in the results section. 


![Alt text](./images/image22.png)


## The Tables
There are two tables now: 
* **Customers**
* **Orders**

### Desired Fields
* **From the Orders table:** `OrderID`, `OrderDate`, and `OrderTotal`
* **From the Customers table:** `CustomerName` and `Phone number`

## How it Works
The two tables (Order Table and Customer Table) are connected to each other with the help of a **`JOIN`**. 

Next, you also need to specify how you are going to join the tables. Once you take a look at the two tables, both of them have a **Customer ID** in common. So, both tables can be joined together with the help of **Customer ID**.


### Using Table Aliases

We can also use **aliases**. For example:
* For `dbo.orders`, we can refer to it as **`o`**
* For `dbo.customers`, we can use an alias as **`c`**

This is more for our **convenience** and for making the code look **cleaner**. There is nothing else in particular to it.

![Alt text](./images/image23.png)


This gives us the exact same result, but the code looks cleaner.

## Understanding JOIN Types

### Inner Join
The `JOIN` written here is an **`INNER JOIN`**. 
* We can explicitly type `INNER JOIN` instead of just `JOIN`. 
* Whenever you type `JOIN` by itself, SQL defaults to an **`INNER JOIN`**.  

An `INNER JOIN` gives us all the customers who have an order, and all the orders that have customers associated with them. If a customer does not have any order, they **will not** show up in an inner join list.

### Right Outer Join
If you want to see a customer who **does not have any orders**, you use a **`RIGHT OUTER JOIN`**. This ensures all records from the right table are included, even if they don't have a matching order.

![Alt text](./images/image24.png)


### Right Outer Join
A **`RIGHT OUTER JOIN`** means that we need to see all the customers irrespective of whether they have orders or not. 

Since `dbo.customers` is present on the right side of the query, we do a right outer join. As a result, the order value in the last row will show as **`NULL`**, but the customer name will still be given.

### Left Outer Join
Similarly, if we want to check all orders irrespective of whether a customer name is present or not, we do a **`LEFT OUTER JOIN`**.


![Alt text](./images/image25.png)


The above data has all the names of the customers in regards to the order details, which is why we cannot see any **`NULL`** values.

## Adding Customer ID and Resolving Ambiguity

Next in the query, I also want to add **`CustomerID`**. 

If we simply type `CustomerID` after `CustomerName` and execute the query, it will give us an **invalid result** (or an ambiguous column error). 

This happens because `CustomerID` exists in **both** tables. SQL does not know whether to pull it from the `Customers` table or the `Orders` table. To fix this, you must specify the table name or its alias before the column name (e.g., `c.CustomerID` or `o.CustomerID`).


![Alt text](./images/image26.png)


### Resolving Column Ambiguity

The reason for the error is that **`CustomerID`** is present in both tables. The query becomes confused about which table it should pull the ID from. 

Hence, we need to explicitly tell the query which of the two tables to use:
* Here, we are going to pull the customer ID from the **Customers** table.
* The alias we mentioned for this table is **`c`**. 

Therefore, we type **`c.CustomerID`**. This resolves the confusion, gives us the correct result, and pulls the data directly from the customer database represented by `c`.


![Alt text](./images/image27.png)

## Sorting Results with ORDER BY

Next, if we want our data to be presented in a specific sequence or order, we use the **`ORDER BY`** clause. 

In this specific example, we want to sort our results by **`OrderTotal`**. 


![Alt text](./images/image28.png)


### Sorting Direction (Ascending vs. Descending)

By default, this gives us the **`OrderTotal`** sorted in **ascending order** (lowest to highest). 

If you want the results in **descending order** (highest to lowest), you just type **`DESC`** after the column name.


![Alt text](./images/image29.png)


## Filtering by Date: Orders from the Past Month

We need to get all the orders from the past month where the order date is exactly one month in the past. 

To achieve this, we need to filter the database to retrieve all orders where the order date occurs **after** that specific date.


![Alt text](./images/image30.png)


### Automating Date Filters with DATEADD

Now we need to see the orders for the past month on an ongoing basis. Because we need to keep on repeating this query, we cannot just go in and manually change the dates every time. 

To solve this, we use a command called **`DATEADD`** which dynamically calculates the date. 

Inside the function:
* **`month`** represents the unit of time we want to change.
* **`-1`** subtracts one month to pull all the orders from the past month.
* **`GETDATE()`** represents the function that pulls the current date and time.


![Alt text](./images/image31.png)


This gives us the exact same results, except now with this function, when we run the same query next week, we will get all the orders of the past month relative to that day. There is absolutely no need to update the date manually.

## Aggregating Data with COUNT

If you want to calculate the total number of orders from the past month rather than listing them individually, you can just add the **`COUNT()`** function to your query.


![Alt text](./images/image32.png)


This gives us the total number of orders in the past month, automatically calculating the timeframe based on the exact day you run the query.

## Totaling Revenue with SUM

Similarly, if you want to calculate the total revenue instead of the number of orders, you can sum up the order totals of the past month by typing **`SUM(OrderTotal)`**.


![Alt text](./images/image33.png)


## Grouping Results with GROUP BY

We can also group all the orders with the help of **`GROUP BY`**. 

This means if *CustomerA* has 4 different orders in a single month, applying `GROUP BY` with the **Customer ID** allows us to aggregate those records and calculate the exact total revenue obtained from that specific customer.


![Alt text](./images/image34.png)





