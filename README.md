# 🏢 Employee Management System

A desktop GUI application built with **Java Swing** and **MySQL** that provides a complete CRUD interface for managing employee records within an organization.

---

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Project Structure](#project-structure)
- [Technology Stack](#technology-stack)
- [Database Schema](#database-schema)
- [Prerequisites](#prerequisites)
- [Setup & Installation](#setup--installation)
- [Running the Application](#running-the-application)
- [Application Flow](#application-flow)
- [Dependencies](#dependencies)

---

## Overview

The **Employee Management System** is a Java-based desktop application that enables HR administrators and managers to efficiently manage employee data. It features a multi-screen GUI with a splash screen, secure login, and full employee lifecycle management (add, view, update, remove).

---

## ✨ Features

| Feature | Description |
|---|---|
| 🔐 **Secure Login** | Username/password authentication backed by a MySQL database |
| ➕ **Add Employee** | Register new employees with complete personal and professional details |
| 👁️ **View Employees** | Browse all employee records in a sortable/scrollable table; search by Employee ID |
| ✏️ **Update Employee** | Modify editable fields (father's name, salary, address, phone, email, education, designation) |
| 🗑️ **Remove Employee** | Delete an employee record by selecting their ID from a dropdown |
| 🖨️ **Print Records** | Print the current employee table view directly from the application |
| 🎨 **Splash Screen** | Animated blinking title screen with a "Click Here to Continue" button |
| 🆔 **Auto Employee ID** | Automatically generates a unique 6-digit random Employee ID on record creation |

---

## 📁 Project Structure

```
java/
├── Splash.java           # Entry point — animated splash screen
├── Login.java            # User authentication screen
├── Home.java             # Main dashboard with navigation buttons
├── AddEmployee.java      # Form to register a new employee
├── ViewEmployee.java     # Table view of all employees; search & print
├── UpdateEmployee.java   # Form to edit existing employee details
├── RemoveEmployee.java   # Screen to delete an employee record
└── Conn.java             # MySQL database connection utility
```

---

## 🛠️ Technology Stack

- **Language:** Java (JDK 8+)
- **GUI Framework:** Java Swing (`javax.swing`, `java.awt`)
- **Database:** MySQL
- **JDBC Driver:** MySQL Connector/J (`com.mysql.cj.jdbc.Driver`)
- **Date Picker:** JCalendar (`com.toedter.calendar.JDateChooser`)
- **Table Utility:** rs2xml (`net.proteanit.sql.DbUtils`) — converts `ResultSet` to `TableModel`

---

## 🗄️ Database Schema

The application connects to a MySQL database named **`employeemanagementsystem`**.

### Table: `employee`

| Column | Type | Description |
|---|---|---|
| `name` | VARCHAR | Employee's full name |
| `fname` | VARCHAR | Father's name |
| `dob` | VARCHAR | Date of birth |
| `salary` | VARCHAR | Monthly salary |
| `address` | VARCHAR | Residential address |
| `phone` | VARCHAR | Contact number |
| `email` | VARCHAR | Email address |
| `education` | VARCHAR | Highest qualification |
| `designation` | VARCHAR | Job title/role |
| `aadhar` | VARCHAR | Aadhaar (national ID) number |
| `empId` | VARCHAR | Unique Employee ID (auto-generated) |

### Table: `login`

| Column | Type | Description |
|---|---|---|
| `username` | VARCHAR | Admin username |
| `password` | VARCHAR | Admin password |

### SQL to Create the Database

```sql
CREATE DATABASE employeemanagementsystem;

USE employeemanagementsystem;

CREATE TABLE employee (
    name        VARCHAR(100),
    fname       VARCHAR(100),
    dob         VARCHAR(30),
    salary      VARCHAR(20),
    address     VARCHAR(200),
    phone       VARCHAR(15),
    email       VARCHAR(100),
    education   VARCHAR(50),
    designation VARCHAR(100),
    aadhar      VARCHAR(20),
    empId       VARCHAR(10) PRIMARY KEY
);

CREATE TABLE login (
    username VARCHAR(50),
    password VARCHAR(50)
);

-- Insert a default admin user
INSERT INTO login VALUES ('admin', 'admin123');
```

---

## ✅ Prerequisites

Before running this project, ensure you have the following installed:

1. **Java JDK 8 or higher** — [Download here](https://www.oracle.com/java/technologies/downloads/)
2. **MySQL Server** — [Download here](https://dev.mysql.com/downloads/mysql/)
3. **MySQL Connector/J** JAR — `mysql-connector-j-x.x.x.jar`
4. **JCalendar** JAR — `jcalendar-1.4.jar` (or latest)
5. **rs2xml** JAR — `rs2xml.jar`

---

## ⚙️ Setup & Installation

### 1. Clone or Download the Project

```bash
git clone <repository-url>
cd java
```

### 2. Set Up the MySQL Database

Start your MySQL server, then run the SQL script above (or use MySQL Workbench) to create the database, tables, and a default login user.

### 3. Configure the Database Connection

Open [`Conn.java`](./Conn.java) and update the credentials if needed:

```java
c = DriverManager.getConnection(
    "jdbc:mysql:///employeemanagementsystem",
    "root",          // ← your MySQL username
    "yourpassword"   // ← your MySQL password
);
```

### 4. Add Required JAR Files to Classpath

Place the following JARs in a `lib/` folder and add them to your project build path:
- `mysql-connector-j-x.x.x.jar`
- `jcalendar-1.4.jar`
- `rs2xml.jar`

### 5. Add Icon Assets

Create an `icons/` folder in your source/resource root with the following images:
- `icons/front.jpg` — Background image for the splash screen
- `icons/second.jpg` — Image shown on the login screen
- `icons/home.jpg` — Background image for the home dashboard
- `icons/delete.png` — Image shown on the remove employee screen

---

## ▶️ Running the Application

### Using an IDE (IntelliJ IDEA / Eclipse / NetBeans)

1. Open the project in your IDE.
2. Add all JAR dependencies to the build path.
3. Set `Splash.java` as the main entry point.
4. Run the project.

### Using Command Line

```bash
# Compile all Java files (adjust classpaths to your JAR locations)
javac -cp ".;lib/*" employee/management/system/*.java

# Run the application
java -cp ".;lib/*" employee.management.system.Splash
```

> **Note:** On Linux/macOS, replace `;` with `:` in the classpath separator.

---

## 🔄 Application Flow

```
Splash Screen
     │
     ▼  (Click "CLICK HERE TO CONTINUE")
Login Screen
     │
     ▼  (Enter valid username & password)
Home Dashboard
     ├──► Add Employee    → Fill form → Save → Home
     ├──► View Employees  → Browse table → Search / Print / Update / Back
     │                              └──► Update Employee → Edit → Save → Home
     └──► Remove Employee → Select ID → Delete → Home
```

---

## 📦 Dependencies

| Library | Purpose |
|---|---|
| `mysql-connector-j` | JDBC driver to connect Java with MySQL |
| `jcalendar` | Provides the `JDateChooser` date picker widget in the Add Employee form |
| `rs2xml` | Converts `ResultSet` objects into a `TableModel` for use with `JTable` |

---

## ⚠️ Notes & Known Issues

- The application uses **string concatenation in SQL queries** which makes it vulnerable to SQL injection. For production use, replace with `PreparedStatement`.
- Passwords in the `login` table are stored in **plain text**. Consider hashing with BCrypt for real deployments.
- The database password is **hardcoded** in `Conn.java`. Move it to a config file or environment variable for better security.
- The Update Employee screen navigates via `ViewEmployee` when the "Update Employee" button is clicked from the Home screen.

---

## 👨‍💻 Author

**Vedant Gaikwad**

---

## 📄 License

This project is intended for educational purposes.
