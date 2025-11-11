# Online Student Management System

## 📚 Project Overview
A comprehensive Spring and Hibernate-based Student Management System demonstrating:
- **Dependency Injection** using Spring Java-based configuration
- **CRUD Operations** using Hibernate ORM
- **Transaction Management** for fee payment and refund operations
- **Layered Architecture** (Model-DAO-Service-Controller)

## 🎯 Features
1. **Student Management**: Add, Update, Delete, and View student records
2. **Course Management**: Manage course offerings and assignments
3. **Fee Management**: Handle fee payments and refunds with transaction safety
4. **Enrollment System**: Enroll students in courses with dependency injection

## 🏗️ Project Structure

```
online-student-management-system/
├── src/
│   └── main/
│       ├── java/
│       │   └── com/
│       │       └── studentmanagement/
│       │           ├── model/          # Entity classes
│       │           │   ├── Student.java
│       │           │   ├── Course.java
│       │           │   └── Payment.java
│       │           ├── dao/            # Data Access Layer
│       │           │   ├── StudentDAO.java
│       │           │   ├── CourseDAO.java
│       │           │   └── PaymentDAO.java
│       │           ├── service/        # Service Layer
│       │           │   ├── StudentService.java
│       │           │   └── FeeService.java
│       │           ├── config/         # Spring Configuration
│       │           │   └── AppConfig.java
│       │           └── MainApp.java    # Main Application
│       └── resources/
│           ├── hibernate.cfg.xml
│           └── database-schema.sql
├── pom.xml
└── README.md
```

## 🔧 Technologies Used

| Technology | Version | Purpose |
|------------|---------|----------|
| Java | 11+ | Programming Language |
| Spring Framework | 5.3.30 | DI & IoC Container |
| Hibernate | 5.6.15 | ORM Framework |
| MySQL | 8.0+ | Database |
| Maven | 3.6+ | Build Tool |
| SLF4J/Logback | 2.0/1.4 | Logging |

## 📦 Dependencies

All dependencies are managed in `pom.xml`:
- Spring Core, Context, ORM, TX
- Hibernate Core
- MySQL Connector
- H2 Database (for testing)
- Apache Commons DBCP2 (Connection Pooling)
- Logging frameworks

## ⚙️ Setup Instructions

### Prerequisites
1. JDK 11 or higher
2. Maven 3.6+
3. MySQL 8.0+
4. IDE (IntelliJ IDEA / Eclipse)

### Database Setup
```sql
CREATE DATABASE student_management_db;
USE student_management_db;
```

Run the schema from `src/main/resources/database-schema.sql`

### Configuration
1. Update database credentials in `hibernate.cfg.xml`:
```xml
<property name="hibernate.connection.url">jdbc:mysql://localhost:3306/student_management_db</property>
<property name="hibernate.connection.username">your_username</property>
<property name="hibernate.connection.password">your_password</property>
```

### Build and Run
```bash
# Clone the repository
git clone https://github.com/Nishant10010/online-student-management-system.git
cd online-student-management-system

# Build the project
mvn clean install

# Run the application
mvn exec:java -Dexec.mainClass="com.studentmanagement.MainApp"
```

## 💡 Key Concepts Demonstrated

### 1. Dependency Injection (DI)
**Spring Java Configuration**:
```java
@Configuration
@EnableTransactionManagement
public class AppConfig {
    @Bean
    public Course javaCourse() {
        return new Course("Java Programming", 6);
    }
    
    @Bean
    public Student student(Course course) {
        Student student = new Student("John Doe", "john@example.com", "1234567890");
        student.setCourse(course);  // DI via setter
        return student;
    }
}
```

### 2. CRUD Operations
**StudentDAO Example**:
```java
public class StudentDAO {
    // Create
    public void saveStudent(Student student);
    
    // Read
    public Student getStudentById(Long id);
    public List<Student> getAllStudents();
    
    // Update
    public void updateStudent(Student student);
    
    // Delete
    public void deleteStudent(Long id);
}
```

### 3. Transaction Management
**FeeService with @Transactional**:
```java
@Service
public class FeeService {
    @Transactional
    public void processPayment(Long studentId, BigDecimal amount) {
        // Multiple operations in single transaction
        // Automatic rollback on exception
    }
    
    @Transactional
    public void processRefund(Long studentId, BigDecimal amount) {
        // Transaction ensures data consistency
    }
}
```

## 🎮 Usage Example

### Console Menu
```
=== Student Management System ===
1. Add New Student
2. View All Students
3. Update Student
4. Delete Student
5. Enroll Student in Course
6. Process Fee Payment
7. Process Refund
8. Exit
Enter your choice:
```

## 📊 Database Schema

### Tables
1. **students**: student_id, name, email, phone, course_id, balance, enrollment_status
2. **courses**: course_id, course_name, duration
3. **payments**: payment_id, student_id, amount, payment_date, payment_type

## 🔍 Testing

Run unit tests:
```bash
mvn test
```

## 📝 Code Files

### Complete Code Available
All source code files are included in the repository:
- Entity Classes (Model Layer)
- DAO Classes (Data Access Layer)
- Service Classes (Business Logic)
- Configuration Files
- Main Application

## 🤝 Contributing
Feel free to fork this repository and submit pull requests.

## 📄 License
This project is for educational purposes.

## 👨‍💻 Author
**Nishant10010** (Aayush Kumar)

## 📧 Contact
For questions or issues, please create an issue in the repository.

---

### 🎯 Learning Outcomes
✅ Understanding Spring Dependency Injection
✅ Implementing Hibernate ORM mappings
✅ Managing transactions with Spring @Transactional
✅ Building layered architecture applications
✅ Working with relational databases using JPA/Hibernate

**Happy Learning! 🚀**
