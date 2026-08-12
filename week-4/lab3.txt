import java.sql.*;

public class JDBCStoredProcDemo {
    public static void main(String[] args) {
        String url = "jdbc:mysql://localhost:3306/your_database"; // change DB name
        String user = "root"; // change username
        String password = "root"; // change password

        try (Connection conn = DriverManager.getConnection(url, user, password)) {
            System.out.println("Database connected.");

            // 1. Call insert_employee procedure
            CallableStatement insertStmt = conn.prepareCall("{call insert_employee(?, ?, ?)}");
            insertStmt.setInt(1, 101); // emp_id
            insertStmt.setString(2, "John Doe"); // emp_name
            insertStmt.setDouble(3, 55000.00); // salary
            insertStmt.execute();
            System.out.println("Record inserted successfully.");

            // 2. Call get_salary_by_id procedure
            CallableStatement getSalaryStmt = conn.prepareCall("{call get_salary_by_id(?, ?)}");
            getSalaryStmt.setInt(1, 101); // input emp_id
            getSalaryStmt.registerOutParameter(2, Types.DECIMAL); // output param
            getSalaryStmt.execute();

            double salary = getSalaryStmt.getDouble(2);
            System.out.println("Salary for Employee ID 101 is: " + salary);

            // Close resources
            insertStmt.close();
            getSalaryStmt.close();

        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}

