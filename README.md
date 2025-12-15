🧾 Online Job Portal – Java Project (Semester 3)

A fully functional Java Web Application that connects Employers, Job Seekers, and Admins through an online job portal.
Built using JSP, Servlets, JDBC, MySQL, Maven, and Tomcat, this project strictly follows the academic rubric requirements:
✔ OOP
✔ Collections & Generics
✔ Multithreading
✔ JDBC (CRUD + PreparedStatements)
✔ Transaction Management
✔ MVC Architecture

🚀 Project Overview

This Online Job Portal allows:

👨‍💼 Employers

Post new job listings

View and manage their posted jobs

Delete job postings

Review applications submitted by job seekers

👨‍💻 Job Seekers

View and search approved job listings

Apply to jobs

Track their application statuses

🛠️ Admin

Manage all users (add / delete / assign roles)

Approve or reject job postings

Oversee system activity

Maintain database integrity

🏗️ Features Implemented (Matches Rubric)
✔ 1. OOP Concepts (Polymorphism, Encapsulation, Inheritance, Interfaces)

Model classes: User, Job, Application

DAO pattern for database abstraction

Servlets as controllers (MVC architecture)

✔ 2. Collections & Generics

Uses List<Job>, List<Application>, etc.

Uses ConcurrentLinkedQueue for thread-safe notifications

✔ 3. Multithreading & Synchronization

NotificationWorker background thread

Thread-safe queue for notifications

✔ 4. JDBC + CRUD + PreparedStatement

Secure SQL operations

Insert, Update, Delete, Select implemented in DAOs

✔ 5. Transaction Management

Admin job approval uses manual transaction commit/rollback

✔ 6. MVC Architecture

JSP (View)

Servlets (Controller)

DAO classes (Model/Database Layer)

📁 Project Structure
.
├── sql/
│   └── schema.sql
├── src/main/java/com/example/jobportal/
│   ├── dao/
│   │   ├── JobDAO.java
│   │   ├── UserDAO.java
│   │   └── ApplicationDAO.java
│   ├── model/
│   │   ├── Job.java
│   │   ├── User.java
│   │   └── Application.java
│   ├── servlet/
│   │   ├── AdminUserServlet.java
│   │   ├── EmployerJobServlet.java
│   │   ├── JobSeekerServlet.java
│   │   ├── IndexServlet.java
│   │   └── AppContextListener.java
│   ├── worker/
│   │   └── NotificationWorker.java
│   └── util/
│       └── DBConnectionPool.java
├── src/main/webapp/
│   ├── index.jsp
│   ├── admin/admin-dashboard.jsp
│   ├── employer/employer-dashboard.jsp
│   ├── jobseeker/jobseeker-dashboard.jsp
│   └── WEB-INF/web.xml
├── pom.xml
└── README.md

🐳 Docker Setup (Recommended)

This project uses **Docker Compose** for easy setup with containerized MySQL and Tomcat.

### Prerequisites
- Docker Desktop installed and running
- Java 11+ (for Maven build)
- Maven 3.6+ installed

### Quick Start

**Option 1: Using Batch Scripts (Windows)**

```batch
# Start the entire application (database + web app)
start-app.bat

# Access the application at:
# http://localhost:8081/online-job-portal/
```

**Option 2: Manual Docker Commands**

```bash
# Build the WAR file
mvn clean package

# Start all containers
docker-compose up -d

# Check container status
docker-compose ps

# View logs
docker-compose logs -f

# Stop containers
docker-compose down
```

### Port Configuration
- **MySQL**: Port 3308 (to avoid conflicts with local MySQL on 3306)
- **Tomcat**: Port 8081 (to avoid conflicts with local Tomcat on 8080)

### Database Details
- **Host**: mysql (internal Docker network) / localhost:3308 (from host machine)
- **Database**: job_portal
- **Username**: root
- **Password**: root
- **JDBC URL**: `jdbc:mysql://mysql:3306/job_portal?useSSL=false&serverTimezone=UTC&allowPublicKeyRetrieval=true`

### Default Admin Account
- **Email**: admin@example.com
- **Password**: adminpass

### Database Tables Created Automatically
- users
- jobs
- applications
- job_audit (for transaction management)

🧩 How to Build & Run

### Development Mode (Docker)

```bash
# 1. Build the project
mvn clean package

# 2. Start Docker containers
docker-compose up -d --build

# 3. Wait for containers to be healthy (check with):
docker-compose ps

# 4. Open browser
http://localhost:8081/online-job-portal/
```

### Production Mode (Manual Tomcat - Without Docker)

If you prefer not to use Docker, follow these steps to run the application with local MySQL and Tomcat:

#### Prerequisites
- **MySQL 8.0+** installed and running on localhost:3306
- **Apache Tomcat 10.1+** installed
- **Java 11+** (JDK)
- **Maven 3.6+** installed

#### Step-by-Step Setup

**1. Configure Database Connection**

Edit `src/main/resources/db.properties`:

```properties
jdbc.url=jdbc:mysql://localhost:3306/job_portal?useSSL=false&serverTimezone=UTC&allowPublicKeyRetrieval=true
jdbc.user=root
jdbc.password=YOUR_MYSQL_PASSWORD
jdbc.maxPoolSize=10
```

**2. Create Database and Tables**

```bash
# Login to MySQL
mysql -u root -p

# Create database
CREATE DATABASE job_portal;

# Exit MySQL
exit

# Run schema file
mysql -u root -p job_portal < sql/schema.sql
```

This creates:
- `users` table (with default admin: admin@example.com / adminpass)
- `jobs` table
- `applications` table
- `job_audit` table

**3. Build the Project**

```bash
mvn clean package
```

This generates: `target/online-job-portal.war`

**4. Deploy to Tomcat**

```bash
# Copy WAR file to Tomcat webapps directory
# Windows:
copy target\online-job-portal.war C:\path\to\tomcat\webapps\

# Linux/macOS:
cp target/online-job-portal.war /path/to/tomcat/webapps/
```

**5. Start Tomcat**

```bash
# Windows:
cd C:\path\to\tomcat\bin
startup.bat

# Linux/macOS:
cd /path/to/tomcat/bin
./startup.sh
```

**6. Access the Application**

Open your browser:
```
http://localhost:8080/online-job-portal/
```

**Login as Admin:**
- Email: `admin@example.com`
- Password: `adminpass`

#### Troubleshooting (Non-Docker Setup)

**Issue: Port 8080 already in use**
- Solution: Edit `conf/server.xml` in Tomcat directory and change the Connector port to 8081 or another available port

**Issue: Database connection failed**
- Verify MySQL is running: `mysql -u root -p`
- Check credentials in `db.properties` match your MySQL setup
- Ensure `job_portal` database exists

**Issue: WAR not deploying**
- Check Tomcat logs: `logs/catalina.out` (Linux/macOS) or `logs/catalina.log` (Windows)
- Ensure Tomcat version is 10.1+ (for Jakarta Servlet API)
- Verify WAR file was copied correctly to `webapps/`


Dashboards:

- **Admin** → Login at `/login` with admin@example.com / adminpass
- **Employer** → `/employer/employer-dashboard.jsp`
- **Job Seeker** → `/jobseeker/jobseeker-dashboard.jsp`

### Application URLs

- **Main Page**: http://localhost:8081/online-job-portal/
- **Login Page**: http://localhost:8081/online-job-portal/login
- **Admin Dashboard**: http://localhost:8081/online-job-portal/admin/admin-dashboard.jsp
- **Employer Dashboard**: http://localhost:8081/online-job-portal/employer/employer-dashboard.jsp
- **Job Seeker Dashboard**: http://localhost:8081/online-job-portal/jobseeker/jobseeker-dashboard.jsp

🔍 Testing Tips

- **Docker Status**: Run `docker-compose ps` to verify both containers are healthy
- **Database Connection**: MySQL Connector/J 8.0.33 with allowPublicKeyRetrieval=true parameter
- **View Logs**: 
  - Tomcat: `docker-compose logs tomcat`
  - MySQL: `docker-compose logs mysql`
- **Restart Containers**: `docker-compose restart`
- **Clean Restart**: `docker-compose down && docker-compose up -d --build`
- **Login as Admin**: Use admin@example.com / adminpass to access admin features
- **Avoid Duplicate Users**: Each email must be unique (enforced by database constraint)

🛠️ Troubleshooting

**Port Conflicts**
- If ports 3308 or 8081 are in use, modify `docker-compose.yml`
- Change ports to available ones (e.g., 3309:3306 or 8082:8080)

**Database Connection Issues**
- Ensure Docker containers are running: `docker-compose ps`
- Check db.properties has correct JDBC URL with `allowPublicKeyRetrieval=true`
- Verify MySQL container is healthy: `docker-compose logs mysql`

**WAR Not Deploying**
- Check Maven build succeeded: Look for `BUILD SUCCESS`
- Verify WAR exists: `ls target/online-job-portal.war`
- Rebuild containers: `docker-compose up -d --build`

**Missing Dependencies**
- MySQL driver included via maven-dependency-plugin
- All dependencies copied to WEB-INF/lib automatically during build

🧠 Project Files & Scripts

### Batch Scripts (Windows)
- **start-app.bat** - Builds and starts the entire application
- **stop-app.bat** - Stops all Docker containers

### Docker Files
- **Dockerfile** - Tomcat 10.1 container configuration
- **Dockerfile.mysql** - MySQL 8.0 container configuration
- **docker-compose.yml** - Multi-container orchestration

🎯 Key Technical Implementations

### Database Connection Pool
- **HikariCP 5.0.1** - High-performance JDBC connection pooling
- **Explicit Driver Loading** - `Class.forName("com.mysql.cj.jdbc.Driver")`
- **Connection Parameters** - allowPublicKeyRetrieval=true for Docker networking

### Authentication System
- **LoginServlet.java** - Session-based authentication
- **LogoutServlet.java** - Session cleanup
- **Role-based Routing** - Redirects based on user role (admin/employer/seeker)

### Transaction Management
- **Manual Commit/Rollback** - Admin job approval with audit logging
- **PreparedStatements** - SQL injection protection
- **Connection Pool** - Efficient resource management

### Multithreading
- **NotificationWorker** - Background thread for async notifications
- **ConcurrentLinkedQueue** - Thread-safe notification queue

✅ Conclusion

This project demonstrates practical knowledge of:

✔ Java Web Development (JSP + Servlets)
✔ JDBC CRUD Operations with PreparedStatements
✔ OOP Principles (Encapsulation, Inheritance, Polymorphism)
✔ Collections & Generics
✔ Multithreading & Synchronization
✔ Transaction Management
✔ MVC Architecture
✔ Maven Build Tool
✔ Docker Containerization
✔ Connection Pooling with HikariCP
✔ Session Management & Authentication

**Deployment Status**: ✅ Successfully deployed and tested with Docker
**Database**: ✅ MySQL 8.0 running on port 3308
**Application**: ✅ Tomcat 10.1 running on port 8081
**Access URL**: http://localhost:8081/online-job-portal/

A complete academic + production-ready Java Web Application.
