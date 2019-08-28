## JDBC Questions for 12-2

### 1) Steps to connect to database server using JDBC

- Assumed: You have a SQL server running, and the JDBC driver (`mysql-connector-java-8.0.17.jar` for example)
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

Example code for executeQuery():

		String selectQuery;
		Connection con = DBConnection.getDBInstance();
		DBUtility.useDB(con, "employee_servlet");
		
		ResultSet rs;
		
		response.setContentType("text/html");
		
		selectQuery = "SELECT * FROM employee;";
		rs = DBUtility.executeQuery(con, selectQuery);
		response.getWriter().append("<p class=\"data\">" + DBUtility.printEntireRS(rs) + "</p>");

Example code for executeUpdate:

    Statement statement;
		try {
			statement = con.createStatement();
			System.out.println(statement.executeUpdate(query) + " Rows affected.");
			return true;
		}

Example code for next():

    String str = "";
    ResultSetMetaData rsmd;
		try {
			rsmd = rs.getMetaData();
			while (rs.next()) {
				str = str + "<br/>: ";
				for (int i = 1; i <= rsmd.getColumnCount(); i++) {
					str = str + (rs.getString(i) + " : ");
				}
			}
			return str;
			
		}
