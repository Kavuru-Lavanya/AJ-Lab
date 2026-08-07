

1.Check Java version :

&#x09;->java -version

&#x09;

For Java installation :

&#x09;->sudo apt update

&#x09;->sudo apt install default-jdk



Step 2: Install MySQL Server

&#x09;->sudo apt update

&#x09;->sudo apt install mysql-server



&#x09;Start MySQL :

&#x09;	->sudo systemctl start mysql



&#x09;Check status :

&#x09;	->sudo systemctl status mysql

&#x09;

&#x09;Login :

&#x09;	->sudo mysql

&#x09;	Note :It takes to mysql



Step 3: Create Database



&#x09;Inside mysql prompt :

&#x09;	->CREATE DATABASE studentdb;



&#x09;Use database

&#x09;	->USE studentdb;



Step 4: Create Student Table

&#x09;CREATE TABLE student

&#x09;(

&#x20;   		rollno INT PRIMARY KEY,

&#x20;   		name VARCHAR(50),

&#x20;   		address VARCHAR(100)

&#x09;);



&#x09;Verify :

&#x09;	->DESC student;



&#x09;Output :

&#x09;	rollno

&#x09;	name

&#x09;	address



&#x09;Exit mysql :

&#x09;	->exit;



Step 5: Create MySQL User (Recommended)



&#x09;Login :

&#x09;	->sudo mysql

&#x09;Execute :

&#x09;	CREATE USER 'javauser'@'localhost' IDENTIFIED BY 'password123';

&#x09;	GRANT ALL PRIVILEGES ON studentdb.\* TO 'javauser'@'localhost';

&#x09;	FLUSH PRIVILEGES;

&#x09;	EXIT;



Step 6: Download MySQL JDBC Driver

&#x09;

&#x09;Download the MySQL Connector/J JAR from the official site and place it in your 	project folder. My sql connector link:

&#x09;	->https://dev.mysql.com/downloads/connector/j/?os=26\&utm\_source=chatgpt.com

&#x09;

&#x09;Download steps :

&#x09;	Open the link above.

&#x09;	Under Select Operating System, choose Platform Independent.

&#x09;	Download the ZIP Archive (for example, mysql-connector-j-9.7.0.zip).



&#x09;Extract the ZIP:

&#x09;	->unzip mysql-connector-j-9.7.0.zip

&#x09;

&#x09;Go inside the extracted folder:

&#x09;	->cd mysql-connector-j-9.7.0.jar





Step 7: Write Java Program

&#x09;Create a StudentJDBC.java file inside mysql connector connector jar file.

&#x09;

&#x09;StudentJDBC.java



&#x09;	import java.sql.\*;



&#x20;               public class StudentJDBC {



&#x20;                 static final String URL =

&#x20;          	 "jdbc:mysql://localhost:3306/studentdb";



&#x20;            	static final String USER = "javauser";

&#x20;   		static final String PASSWORD = "password123";



&#x20;  		 public static void main(String args\[]) {



&#x20;       	try {



&#x20;          	 Class.forName("com.mysql.cj.jdbc.Driver");



&#x20;           	Connection con =

&#x20;                   DriverManager.getConnection(URL, USER, PASSWORD);



&#x20;          	 Statement stmt = con.createStatement();



&#x20;           	// Insert Records



&#x20;           	stmt.executeUpdate(

&#x20;               	"INSERT INTO student VALUES(101,'Ravi','Hyderabad')");



&#x20;           	stmt.executeUpdate(

&#x20;               	"INSERT INTO student VALUES(102,'Priya','Chennai')");



&#x20;           	stmt.executeUpdate(

&#x20;               	"INSERT INTO student VALUES(103,'Rahul','Bangalore')");

&#x09;

&#x20;           	System.out.println("Records Inserted.");



&#x20;           	// Update



&#x20;           	stmt.executeUpdate(

&#x20;               	"UPDATE student SET address='Delhi' WHERE rollno=102");



&#x20;           	System.out.println("Record Updated.");



&#x20;           	// Delete

&#x09;

&#x20;          	 stmt.executeUpdate(

&#x20;               	"DELETE FROM student WHERE rollno=103");



&#x20;          	 System.out.println("Record Deleted.");



&#x20;          	 // Display



&#x20;          	 ResultSet rs =

&#x20;                   stmt.executeQuery("SELECT \* FROM student");



&#x20;          	 System.out.println();



&#x20;          	 System.out.println("Student Records");



&#x20;          	 while(rs.next())

&#x20;           	{

&#x20;              		 System.out.println(

&#x20;                       rs.getInt("rollno")+"  "+

&#x20;                       rs.getString("name")+"  "+

&#x20;                       rs.getString("address")

&#x20;              		 );

&#x20;          	 }



&#x20;          	 rs.close();

&#x20;          	 stmt.close();

&#x20;          	 con.close();



&#x20;       	}

&#x20;       	catch(Exception e)

&#x20;      	       {

&#x20;           		e.printStackTrace();

&#x20;       	}



&#x20;  	      }



&#x09;    }





Step 8: Compile Program :

&#x09;	->javac -cp .:mysql-connector-j-9.3.0.jar StudentJDBC.java

&#x09;

&#x09;Run program :

&#x09;	->java -cp .:mysql-connector-j-9.3.0.jar StudentJDBC



&#x09;Expected Output :	

&#x09;	Records Inserted.

&#x09;	Record Updated.

&#x09;	Record Deleted.

&#x09;	

&#x09;	Student Records



&#x09;		101 Ravi Hyderabad

&#x09;		102 Priya Delhi



Step 9 :Verify Using MySQL

&#x09;Login :

&#x09;	->mysql -u javauser -p



&#x09;Password :

&#x09;	->password123



&#x09;Use database :

&#x09;	->USE studentdb;



&#x09;Display :

&#x09;	->SELECT \* FROM student;



&#x09;Output :

&#x09;	+--------+-------+-----------+

&#x09;	| rollno | name  | address   |

&#x09;	+--------+-------+-----------+

&#x09;	| 101    | Ravi  | Hyderabad |

&#x09;	| 102    | Priya | Delhi     |

&#x09;	+--------+-------+-----------+

&#x09;	

