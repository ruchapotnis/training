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



