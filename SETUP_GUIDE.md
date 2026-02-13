# 🚀 Complete Setup Guide - Smart Expense Tracker

This guide will walk you through setting up the Smart Expense Tracker application from scratch on your local machine.

## 📋 Table of Contents
1. [Prerequisites](#prerequisites)
2. [Database Setup](#database-setup)
3. [Backend Setup](#backend-setup)
4. [Frontend Setup](#frontend-setup)
5. [Docker Setup](#docker-setup-alternative)
6. [Common Issues](#common-issues)
7. [Testing the Application](#testing-the-application)

## 🔧 Prerequisites

### Required Software
1. **Java Development Kit (JDK) 17+**
   - Download: https://www.oracle.com/java/technologies/downloads/
   - Verify installation: `java -version`

2. **Maven 3.9+**
   - Download: https://maven.apache.org/download.cgi
   - Verify installation: `mvn -version`

3. **Node.js 18+ and npm**
   - Download: https://nodejs.org/
   - Verify installation: `node -v` and `npm -v`

4. **PostgreSQL 15+**
   - Download: https://www.postgresql.org/download/
   - Verify installation: `psql --version`

5. **Git**
   - Download: https://git-scm.com/downloads
   - Verify installation: `git --version`

### Optional (for Docker setup)
- **Docker Desktop**
  - Download: https://www.docker.com/products/docker-desktop

## 💾 Database Setup

### Step 1: Install PostgreSQL
If you haven't installed PostgreSQL yet:
- **Windows**: Use the installer from postgresql.org
- **macOS**: `brew install postgresql@15`
- **Linux**: `sudo apt-get install postgresql-15`

### Step 2: Start PostgreSQL Service
```bash
# Windows: Start via Services or
net start postgresql-x64-15

# macOS:
brew services start postgresql@15

# Linux:
sudo systemctl start postgresql
```

### Step 3: Create Database
```bash
# Login to PostgreSQL
psql -U postgres

# In PostgreSQL shell, run:
CREATE DATABASE expense_tracker_db;

# Create user (if needed)
CREATE USER expense_user WITH PASSWORD 'your_password';

# Grant privileges
GRANT ALL PRIVILEGES ON DATABASE expense_tracker_db TO expense_user;

# Exit PostgreSQL shell
\q
```

### Step 4: Verify Database
```bash
psql -U postgres -d expense_tracker_db -c "SELECT version();"
```

## 🔨 Backend Setup

### Step 1: Clone Repository
```bash
git clone https://github.com/yourusername/smart-expense-tracker.git
cd smart-expense-tracker
```

### Step 2: Configure Database Connection
Navigate to `backend/src/main/resources/application.properties` and update:

```properties
# Database Configuration
spring.datasource.url=jdbc:postgresql://localhost:5432/expense_tracker_db
spring.datasource.username=postgres
spring.datasource.password=your_password

# JWT Secret (IMPORTANT: Generate your own for production!)
jwt.secret=404E635266556A586E3272357538782F413F4428472B4B6250645367566B5970
jwt.expiration=86400000
jwt.refresh-expiration=604800000
```

### Step 3: Build Backend
```bash
cd backend
mvn clean install
```

This will:
- Download all dependencies
- Compile the code
- Run tests
- Create a JAR file in `target/` directory

### Step 4: Run Backend
```bash
mvn spring-boot:run
```

Or run the JAR directly:
```bash
java -jar target/smart-expense-tracker-1.0.0.jar
```

### Step 5: Verify Backend
Open browser and visit:
- API: http://localhost:8080
- Swagger UI: http://localhost:8080/swagger-ui.html

You should see the Swagger API documentation page.

## 🎨 Frontend Setup

### Step 1: Install Dependencies
```bash
cd frontend
npm install
```

This will install:
- React and React DOM
- React Router
- Axios
- Tailwind CSS
- Recharts
- And all other dependencies

### Step 2: Configure API URL (if needed)
The frontend is configured to proxy API requests to `http://localhost:8080`.

If your backend runs on a different port, update `frontend/vite.config.js`:

```javascript
export default defineConfig({
  plugins: [react()],
  server: {
    port: 3000,
    proxy: {
      '/api': {
        target: 'http://localhost:YOUR_BACKEND_PORT',
        changeOrigin: true
      }
    }
  }
})
```

### Step 3: Run Frontend
```bash
npm run dev
```

### Step 4: Verify Frontend
Open browser and visit: http://localhost:3000

You should see the login page.

## 🐳 Docker Setup (Alternative)

If you prefer using Docker, follow these steps:

### Step 1: Install Docker
- Download Docker Desktop from https://www.docker.com/products/docker-desktop
- Install and start Docker Desktop

### Step 2: Build and Run
From the project root directory:

```bash
# Build and start all containers
docker-compose up --build

# Or run in detached mode
docker-compose up -d --build
```

This will:
- Create PostgreSQL container
- Build and run backend container
- Build and run frontend container

### Step 3: Access Application
- Frontend: http://localhost:3000
- Backend: http://localhost:8080
- Database: localhost:5432

### Step 4: Stop Containers
```bash
docker-compose down

# To remove volumes as well:
docker-compose down -v
```

## 🐛 Common Issues

### Issue 1: Port Already in Use

**Problem**: Backend fails to start with "Port 8080 is already in use"

**Solution**:
```bash
# Find process using port 8080
# Windows:
netstat -ano | findstr :8080

# macOS/Linux:
lsof -i :8080

# Kill the process
# Windows:
taskkill /PID <PID> /F

# macOS/Linux:
kill -9 <PID>
```

Or change the port in `application.properties`:
```properties
server.port=8081
```

### Issue 2: Database Connection Failed

**Problem**: "Connection refused" or "authentication failed"

**Solutions**:
1. Check if PostgreSQL is running:
   ```bash
   # Windows:
   sc query postgresql-x64-15
   
   # macOS:
   brew services list
   
   # Linux:
   sudo systemctl status postgresql
   ```

2. Verify credentials in `application.properties`
3. Check PostgreSQL is listening on the correct port:
   ```bash
   psql -U postgres -c "SHOW port;"
   ```

### Issue 3: Maven Build Fails

**Problem**: "Failed to execute goal" or dependency errors

**Solutions**:
1. Clear Maven cache:
   ```bash
   mvn clean
   rm -rf ~/.m2/repository
   mvn install
   ```

2. Check Java version:
   ```bash
   java -version
   # Should be 17 or higher
   ```

### Issue 4: Frontend Build Fails

**Problem**: "Module not found" or npm errors

**Solutions**:
1. Delete node_modules and reinstall:
   ```bash
   cd frontend
   rm -rf node_modules package-lock.json
   npm install
   ```

2. Clear npm cache:
   ```bash
   npm cache clean --force
   npm install
   ```

### Issue 5: CORS Errors

**Problem**: "CORS policy: No 'Access-Control-Allow-Origin' header"

**Solution**: Check `SecurityConfig.java` has correct origins configured:
```java
configuration.setAllowedOrigins(Arrays.asList("http://localhost:3000"));
```

## ✅ Testing the Application

### 1. Create Test User
```bash
POST http://localhost:8080/api/auth/register
Content-Type: application/json

{
  "firstName": "Test",
  "lastName": "User",
  "email": "test@example.com",
  "password": "Test@1234",
  "phoneNumber": "+1234567890",
  "currency": "USD",
  "monthlyBudget": 1000
}
```

### 2. Login
```bash
POST http://localhost:8080/api/auth/login
Content-Type: application/json

{
  "email": "test@example.com",
  "password": "Test@1234"
}
```

Copy the `accessToken` from the response.

### 3. Create Expense
```bash
POST http://localhost:8080/api/expenses
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json

{
  "title": "Grocery Shopping",
  "description": "Weekly groceries",
  "amount": 150.50,
  "categoryId": 1,
  "expenseDate": "2024-01-15",
  "paymentMethod": "CREDIT_CARD",
  "merchant": "Whole Foods"
}
```

### 4. Verify in UI
1. Go to http://localhost:3000
2. Login with test credentials
3. You should see the expense in the dashboard

## 🎯 Next Steps

1. **Explore the Application**
   - Create expenses
   - View analytics
   - Set budgets

2. **Customize**
   - Add your own categories
   - Modify colors and themes
   - Add new features

3. **Deploy**
   - Backend: Heroku, Railway, or Render
   - Frontend: Vercel, Netlify
   - Database: Heroku Postgres, Supabase

## 📚 Additional Resources

- [Spring Boot Documentation](https://docs.spring.io/spring-boot/docs/current/reference/html/)
- [React Documentation](https://react.dev/)
- [PostgreSQL Documentation](https://www.postgresql.org/docs/)
- [Tailwind CSS Documentation](https://tailwindcss.com/docs)

## 💡 Tips

1. **Use environment variables** for sensitive data in production
2. **Enable HTTPS** for production deployments
3. **Set up proper logging** for debugging
4. **Create regular database backups**
5. **Monitor application performance**

## 🆘 Need Help?

- Check existing issues: [GitHub Issues](https://github.com/yourusername/smart-expense-tracker/issues)
- Create a new issue with details
- Email: konnurpriyanka710@gmail.com

---

**Happy Coding! 🚀**
