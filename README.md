# OnlineBookStore

A user-friendly Online Bookstore project built with Java, JDBC, and Servlets. This application allows customers to browse, purchase books, and sellers/admins to manage inventory.

**[Watch Setup Guide on YouTube](https://youtu.be/mLFPodZO8Iw)**

---

## 📖 About

A full-featured Online Bookstore where:
- **Customers** can register, login, browse books, add to cart, and checkout with payment receipts
- **Admins/Sellers** can login, add new books, remove books, update quantities and prices, and maintain sales history
- Built with a clean service-oriented architecture using JDBC and HTTP Servlets
- Responsive UI with HTML, CSS, JavaScript, and Bootstrap

---

## ✨ Features

### Customer Features
- User registration and login
- Browse available books
- Add books to cart with quantity selection
- Checkout and payment processing
- Download payment receipts

### Admin/Seller Features
- Admin login and dashboard
- Add new books with details (name, author, price, quantity)
- Remove books from inventory
- Update book quantities and prices
- View sales history

---

## 🛠️ Technologies Used

### Frontend
- HTML5
- CSS3
- JavaScript
- Bootstrap 4+

### Backend
- **Java** (JDK 8+)
- **JDBC** - Database connectivity
- **HTTP Servlets** - Request handling
- **Maven** - Build automation

### Database
- MySQL 5.7+ or PostgreSQL 12+

---

## 📋 Prerequisites

Before setting up the project, ensure you have:

| Tool | Version | Link |
|------|---------|------|
| Git | Latest | [Download](https://git-scm.com/) |
| Java JDK | 8 or higher | [Download](https://www.oracle.com/java/technologies/javase-downloads.html) |
| Apache Maven | 3.6+ | [Download](https://maven.apache.org/download.cgi) |
| MySQL Server | 5.7+ | [Download](https://dev.mysql.com/downloads/mysql/) |
| Tomcat (Optional) | 8.0+ | [Download](https://tomcat.apache.org/download-80.cgi) |

---

## 🚀 Setup & Installation

### Step 1: Clone the Repository
```bash
git clone <repository-url>
cd onlinebookstore-master
```

### Step 2: Configure Database Connection
Edit `src/main/resources/application.properties`:
```properties
db.driver=com.mysql.cj.jdbc.Driver
db.host=jdbc:mysql://localhost
db.port=3306
db.name=onlinebookstore
db.username=root
db.password=your_password
```

### Step 3: Initialize the Database
Open MySQL Command Prompt or MySQL Workbench and run:
```bash
mysql -u root -p
```

Then execute the SQL file:
```mysql
SOURCE setup/CreateDatastore.sql;
```

**OR run manually:**
```mysql
CREATE DATABASE IF NOT EXISTS onlinebookstore;
USE onlinebookstore;

CREATE TABLE IF NOT EXISTS books (
    barcode VARCHAR(100) PRIMARY KEY,
    name TEXT NOT NULL,
    author VARCHAR(100) NOT NULL,
    price INT,
    quantity REAL
);

CREATE TABLE IF NOT EXISTS users (
    username VARCHAR(100) PRIMARY KEY,
    password VARCHAR(100) NOT NULL,
    firstname VARCHAR(100) NOT NULL,
    lastname VARCHAR(100) NOT NULL,
    address TEXT NOT NULL,
    phone VARCHAR(100) NOT NULL,
    mailid VARCHAR(100) NOT NULL,
    usertype INT
);

-- Insert sample data
INSERT INTO books VALUES('9780134190563','The Go Programming Language','Alan A. A. Donovan and Brian W. Kernighan',400,8);

-- Insert default admin (usertype=1 for admin, usertype=2 for customer)
INSERT INTO users VALUES('Admin','Admin','Mr.','Admin','Haldia WB','9584552224521','admin@gmail.com',1);
INSERT INTO users VALUES('shashi','shashi','Shashi','Raj','Bihar','1236547089','shashi@gmail.com',2);
```

### Step 4: Build the Project
Navigate to the project directory and run:
```bash
mvn clean package
```

### Step 5: Run the Application
```bash
java -jar target/dependency/webapp-runner.jar --port 8080 target/onlinebookstore.war
```

### Step 6: Access the Application
Open your browser and navigate to:
```
http://localhost:8080/onlinebookstore
```

---

## 🔐 Default Login Credentials

| Role | Username | Password |
|------|----------|----------|
| Admin/Seller | `Admin` | `Admin` |
| Customer | `shashi` | `shashi` |

You can create additional customer accounts through the registration page.

---

## 🔒 Security Updates

### CVE Vulnerabilities Fixed
This project has been patched for the following critical vulnerabilities:

| CVE | Severity | Description | Fix |
|-----|----------|-------------|-----|
| CVE-2024-1597 | **CRITICAL** | SQL injection via line comment in PostgreSQL JDBC | postgresql 42.3.7 → 42.7.4 |
| CVE-2022-41946 | MEDIUM | Temporary file information disclosure | postgresql 42.3.7 → 42.7.4 |

All dependencies are regularly checked for security vulnerabilities.

---

## 📁 Project Structure

```
onlinebookstore-master/
├── src/main/
│   ├── java/
│   │   ├── com/bittercode/
│   │   │   ├── constant/         # Constants and DB column names
│   │   │   ├── model/            # Entity classes (User, Book, Cart, etc.)
│   │   │   ├── service/          # Business logic interfaces
│   │   │   │   └── impl/         # Service implementations
│   │   │   └── util/             # Utility classes (DBUtil, DatabaseConfig)
│   │   └── servlets/             # HTTP request handlers
│   └── resources/
│       └── application.properties # Database configuration
├── WebContent/
│   ├── *.html                    # Frontend pages
│   ├── styles.css                # Styling
│   ├── META-INF/
│   └── WEB-INF/
│       └── web.xml               # Servlet mapping configuration
├── setup/
│   └── CreateDatastore.sql       # Database initialization script
├── pom.xml                       # Maven dependencies
└── README.md                     # This file
```

---

## 🔧 Building & Running Alternatives

### Using Tomcat Server
1. Place the WAR file in Tomcat's `webapps` folder
2. Start Tomcat: `catalina.bat run` (Windows)
3. Access: `http://localhost:8080/onlinebookstore`

### Using Maven Embedded Server
```bash
mvn tomcat7:run
```

---

## 📝 Database Schema

### Users Table
- **username** (PK): Unique login identifier
- **password**: Login password
- **firstname, lastname**: User's name
- **address**: User's address
- **phone**: Contact number
- **mailid**: Email address
- **usertype**: 1 = Admin/Seller, 2 = Customer

### Books Table
- **barcode** (PK): Unique book identifier
- **name**: Book title
- **author**: Author name
- **price**: Book price
- **quantity**: Available quantity

---

## 🐛 Troubleshooting

| Issue | Solution |
|-------|----------|
| Database connection fails | Check `application.properties` - verify host, port, username, password |
| Admin login not working | Ensure admin user is inserted in `users` table with `usertype=1` |
| Port 8080 already in use | Use different port: `java -jar webapp-runner.jar --port 9090 target/onlinebookstore.war` |
| Maven build fails | Run `mvn clean` then `mvn package` |
| Database doesn't exist | Run the SQL initialization script with correct user privileges |

---

## 📚 Learning Resources

This project demonstrates:
- HTTP Servlets for request/response handling
- JDBC for database operations
- Session management and user authentication
- Service layer architecture
- Frontend form handling and validation
- Bootstrap for responsive design

---

## 📄 License

This is an open-source educational project.

---

## 👥 Contributors

Pull requests are welcome! For major changes, please open an issue first to discuss what you would like to change.

---

**Last Updated:** March 2026  
**Java Version:** 8 LTS  
**Status:** ✅ Production Ready
