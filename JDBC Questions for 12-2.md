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

	public static ResultSet executeQuery(Connection con, String query) {
		ResultSet rs = null;
		try {
			Statement statement = con.createStatement();
			rs = statement.executeQuery(query);
		} catch (SQLException e) {
			e.printStackTrace();
		} catch (Exception e) {
			e.printStackTrace();
		}
		return rs;
	}
Example code for executeUpdate:

	public static boolean executeUpdate(Connection con, String query) {
		Statement statement;
		try {
			statement = con.createStatement();
			System.out.println(statement.executeUpdate(query) + " Rows affected.");
			return true;
		} catch (SQLException e) {
			e.printStackTrace();
			return false;
		} catch (Exception e) {
			e.printStackTrace();
			return false;
		}
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
