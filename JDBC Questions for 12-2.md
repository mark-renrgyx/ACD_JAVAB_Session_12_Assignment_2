## JDBC Questions for 12-2

### 1) Steps to connect to database server using JDBC

- Assumed: You have a SQL server running
- Ensure Driver class exists
	- Class.forName("com.mysql.jdbc.Driver");
- Create a Connection with DriverManager
- Use your Connection to createStatement()
- Execute your statement with Statement member functions executeQuery() or executeUpdate()

### 2) Methods, examples
#### executeQuery
This will execute a query which does not change the database (SELECT statement for example)

#### executeUpdate
This will run a query which can change the database table, such as INSERT, UPDATE, DELETE
#### next

Member function of ResultSet.  Moves the ResultSet's cursor down one row (pointing at the next entry in that database table)
