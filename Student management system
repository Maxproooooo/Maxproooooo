import java.io.FileWriter;
import java.io.IOException;
import java.sql.*;
import java.util.Scanner;

public class StudentManagementSystem {

    // Student class to define student properties
    public static class Student {
        private int id;
        private String name;
        private double grade;
        private int attendance;
        private String assignments;

        public Student(int id, String name, double grade, int attendance, String assignments) {
            this.id = id;
            this.name = name;
            this.grade = grade;
            this.attendance = attendance;
            this.assignments = assignments;
        }

        public int getId() { return id; }
        public String getName() { return name; }
        public double getGrade() { return grade; }
        public int getAttendance() { return attendance; }
        public String getAssignments() { return assignments; }
    }

    // Database handler for CRUD operations
    public static class DatabaseHandler {
        private static final String URL = "jdbc:sqlite:students.db"; // Use for SQLite
        // private static final String URL = "jdbc:mysql://localhost:3306/yourdatabase"; // Use for MySQL
        private Connection connection;

        public DatabaseHandler() {
            try {
                connection = DriverManager.getConnection(URL);
                createTable();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }

        private void createTable() throws SQLException {
            String sql = "CREATE TABLE IF NOT EXISTS students (" +
                         "id INTEGER PRIMARY KEY, " +
                         "name TEXT, " +
                         "grade REAL, " +
                         "attendance INTEGER, " +
                         "assignments TEXT)";
            Statement stmt = connection.createStatement();
            stmt.execute(sql);
        }

        public void addStudent(Student student) throws SQLException {
            String sql = "INSERT INTO students (id, name, grade, attendance, assignments) VALUES (?, ?, ?, ?, ?)";
            PreparedStatement pstmt = connection.prepareStatement(sql);
            pstmt.setInt(1, student.getId());
            pstmt.setString(2, student.getName());
            pstmt.setDouble(3, student.getGrade());
            pstmt.setInt(4, student.getAttendance());
            pstmt.setString(5, student.getAssignments());
            pstmt.executeUpdate();
        }

        public void updateStudent(Student student) throws SQLException {
            String sql = "UPDATE students SET name = ?, grade = ?, attendance = ?, assignments = ? WHERE id = ?";
            PreparedStatement pstmt = connection.prepareStatement(sql);
            pstmt.setString(1, student.getName());
            pstmt.setDouble(2, student.getGrade());
            pstmt.setInt(3, student.getAttendance());
            pstmt.setString(4, student.getAssignments());
            pstmt.setInt(5, student.getId());
            pstmt.executeUpdate();
        }

        public void deleteStudent(int id) throws SQLException {
            String sql = "DELETE FROM students WHERE id = ?";
            PreparedStatement pstmt = connection.prepareStatement(sql);
            pstmt.setInt(1, id);
            pstmt.executeUpdate();
        }

        public ResultSet getAllStudents() throws SQLException {
            String sql = "SELECT * FROM students";
            Statement stmt = connection.createStatement();
            return stmt.executeQuery(sql);
        }
    }

    // Utility methods for file I/O and reporting
    public static void generateReport(DatabaseHandler dbHandler) {
        try (FileWriter fw = new FileWriter("StudentReport.txt")) {
            ResultSet rs = dbHandler.getAllStudents();
            fw.write("Student Performance Report:\n\n");
            while (rs.next()) {
                fw.write("ID: " + rs.getInt("id") + "\n");
                fw.write("Name: " + rs.getString("name") + "\n");
                fw.write("Grade: " + rs.getDouble("grade") + "\n");
                fw.write("Attendance: " + rs.getInt("attendance") + "\n");
                fw.write("Assignments: " + rs.getString("assignments") + "\n\n");
            }
            System.out.println("Report generated: StudentReport.txt");
        } catch (IOException | SQLException e) {
            e.printStackTrace();
        }
    }

    public static void main(String[] args) {
        DatabaseHandler dbHandler = new DatabaseHandler();
        Scanner scanner = new Scanner(System.in);

        while (true) {
            System.out.println("1. Add Student");
            System.out.println("2. Update Student");
            System.out.println("3. Delete Student");
            System.out.println("4. Display All Students");
            System.out.println("5. Generate Performance Report");
            System.out.println("6. Exit");
            System.out.print("Choose an option: ");
            int choice = scanner.nextInt();

            try {
                if (choice == 1) {
                    System.out.print("Enter ID: ");
                    int id = scanner.nextInt();
                    scanner.nextLine(); // consume newline
                    System.out.print("Enter Name: ");
                    String name = scanner.nextLine();
                    System.out.print("Enter Grade: ");
                    double grade = scanner.nextDouble();
                    System.out.print("Enter Attendance: ");
                    int attendance = scanner.nextInt();
                    scanner.nextLine(); // consume newline
                    System.out.print("Enter Assignments: ");
                    String assignments = scanner.nextLine();
                    dbHandler.addStudent(new Student(id, name, grade, attendance, assignments));
                    System.out.println("Student added successfully.");
                } else if (choice == 2) {
                    System.out.print("Enter ID of student to update: ");
                    int id = scanner.nextInt();
                    scanner.nextLine();
                    System.out.print("Enter New Name: ");
                    String name = scanner.nextLine();
                    System.out.print("Enter New Grade: ");
                    double grade = scanner.nextDouble();
                    System.out.print("Enter New Attendance: ");
                    int attendance = scanner.nextInt();
                    scanner.nextLine();
                    System.out.print("Enter New Assignments: ");
                    String assignments = scanner.nextLine();
                    dbHandler.updateStudent(new Student(id, name, grade, attendance, assignments));
                    System.out.println("Student updated successfully.");
                } else if (choice == 3) {
                    System.out.print("Enter ID of student to delete: ");
                    int id = scanner.nextInt();
                    dbHandler.deleteStudent(id);
                    System.out.println("Student deleted successfully.");
                } else if (choice == 4) {
                    ResultSet rs = dbHandler.getAllStudents();
                    while (rs.next()) {
                        System.out.println("ID: " + rs.getInt("id"));
                        System.out.println("Name: " + rs.getString("name"));
                        System.out.println("Grade: " + rs.getDouble("grade"));
                        System.out.println("Attendance: " + rs.getInt("attendance"));
                        System.out.println("Assignments: " + rs.getString("assignments"));
                        System.out.println("--------------------------");
                    }
                } else if (choice == 5) {
                    generateReport(dbHandler);
                } else if (choice == 6) {
                    break;
                } else {
                    System.out.println("Invalid option. Try again.");
                }
            } catch (SQLException e) {
                System.out.println("Database error: " + e.getMessage());
            }
        }
        scanner.close();
    }
}

<!--
**Maxproooooo/Maxproooooo** is a ✨ _special_ ✨ repository because its `README.md` (this file) appears on your GitHub profile.

Here are some ideas to get you started:

- 🔭 I’m currently working on ...
- 🌱 I’m currently learning ...
- 👯 I’m looking to collaborate on ...
- 🤔 I’m looking for help with ...
- 💬 Ask me about ...
- 📫 How to reach me: ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...
-->
