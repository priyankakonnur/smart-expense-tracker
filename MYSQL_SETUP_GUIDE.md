# 🚀 Complete MySQL Setup Guide - Smart Expense Tracker

Follow these steps **exactly** to run your project with MySQL!

---

## 📋 STEP 1: Download and Extract Project

### 1.1 Download
- Download the project ZIP/TAR file
- Save to Desktop or Documents folder

### 1.2 Extract
**Windows:** Right-click → Extract All  
**Mac/Linux:** 
```bash
tar -xzf smart-expense-tracker.tar.gz
cd smart-expense-tracker
```

---

## 💻 STEP 2: Install Required Software

### 2.1 Install Java 17 ☕

**Windows:**
1. Go to: https://www.oracle.com/java/technologies/downloads/#java17
2. Download "Windows x64 Installer"
3. Run installer → Keep clicking Next
4. **Verify:**
   ```cmd
   java -version
   ```
   Should show: `java version "17.x.x"`

**Mac:**
```bash
brew install openjdk@17
```

**Linux:**
```bash
sudo apt update
sudo apt install openjdk-17-jdk
java -version
```

---

### 2.2 Install Maven 🔨

**Windows:**
1. Download: https://maven.apache.org/download.cgi
2. Get `apache-maven-3.9.x-bin.zip`
3. Extract to `C:\Program Files\Apache\maven`
4. **Add to PATH:**
   - Windows Search → "Environment Variables"
   - Edit "Path" in System Variables
   - Add: `C:\Program Files\Apache\maven\bin`
5. **Restart Command Prompt** and verify:
   ```cmd
   mvn -version
   ```

**Mac:**
```bash
brew install maven
mvn -version
```

**Linux:**
```bash
sudo apt install maven
mvn -version
```

---

### 2.3 Install Node.js 📦

1. Go to: https://nodejs.org/
2. Download **LTS version** (20.x)
3. Run installer → Keep defaults
4. **Verify:**
   ```bash
   node -v
   npm -v
   ```

---

### 2.4 Install MySQL 🗄️

**Windows:**
1. Download: https://dev.mysql.com/downloads/installer/
2. Get "MySQL Installer" (mysql-installer-community-8.x.x.msi)
3. Run installer
4. Choose "Developer Default" setup type
5. **IMPORTANT:** Set root password to `root` (or remember your password)
6. Keep default port: `3306`
7. Complete installation
8. **Verify:**
   ```cmd
   mysql --version
   ```

**Mac:**
```bash
brew install mysql@8.0
brew services start mysql@8.0

# Secure installation (optional but recommended)
mysql_secure_installation
# Set root password to: root
```

**Linux (Ubuntu/Debian):**
```bash
sudo apt update
sudo apt install mysql-server

# Start MySQL
sudo systemctl start mysql
sudo systemctl enable mysql

# Secure installation
sudo mysql_secure_installation
# Set root password to: root
```

---

## 🗄️ STEP 3: Setup MySQL Database

### 3.1 Login to MySQL

**Windows:**
```cmd
mysql -u root -p
```
Enter password: `root`

**Mac/Linux:**
```bash
mysql -u root -p
```
Enter password: `root`

### 3.2 Create Database

In MySQL shell, run:

```sql
CREATE DATABASE expense_tracker_db;
```

You should see: `Query OK, 1 row affected`

**Verify database was created:**
```sql
SHOW DATABASES;
```

You should see `expense_tracker_db` in the list.

**Exit MySQL:**
```sql
exit;
```

---

## ⚙️ STEP 4: Configure the Backend

### 4.1 Navigate to Project
```bash
cd smart-expense-tracker/backend
```

### 4.2 Update Configuration

Open: `src/main/resources/application.properties`

**Check these settings are correct:**
```properties
spring.datasource.url=jdbc:mysql://localhost:3306/expense_tracker_db?createDatabaseIfNotExist=true&useSSL=false&allowPublicKeyRetrieval=true&serverTimezone=UTC
spring.datasource.username=root
spring.datasource.password=root
```

**If you used a different password, update it here!**

**Save the file.**

---

## 🔨 STEP 5: Run the Backend

### 5.1 Build Project

From `backend` folder:

```bash
mvn clean install
```

⏳ **This takes 3-5 minutes first time** - downloads all dependencies.

**Wait for:**
```
[INFO] BUILD SUCCESS
```

If you see errors, check:
- Java version is 17
- Maven is installed correctly
- You're in the `backend` folder

### 5.2 Run Backend

```bash
mvn spring-boot:run
```

⏳ **Wait 20-30 seconds** for startup.

**Success message:**
```
Started SmartExpenseTrackerApplication in X.XXX seconds
```

**You should also see:**
```
Tomcat started on port(s): 8080
```

✅ **Backend is running!**

**🚨 IMPORTANT: Keep this terminal window OPEN!**

---

## 🎨 STEP 6: Run the Frontend

### 6.1 Open NEW Terminal

**Windows:** Press `Windows + R` → type `cmd` → Enter

**Mac/Linux:** Open new Terminal window

### 6.2 Navigate to Frontend

```bash
cd smart-expense-tracker/frontend
```

### 6.3 Install Dependencies

```bash
npm install
```

⏳ **This takes 2-3 minutes** - installs all packages.

**Wait for completion!**

### 6.4 Start Frontend

```bash
npm run dev
```

**Success message:**
```
  ➜  Local:   http://localhost:3000/
  ➜  Network: use --host to expose
```

✅ **Frontend is running!**

**🚨 IMPORTANT: Keep this terminal window OPEN too!**

---

## ✅ STEP 7: Test the Application

### 7.1 Open Browser

Go to: **http://localhost:3000**

You should see:
- 🎨 Beautiful login page
- 💙 Blue gradient background
- 💰 Dollar sign icon
- 📧 Email and password fields

### 7.2 Create Your Account

1. Click **"Sign up now"** link at bottom
2. Fill registration form:
   - First Name: `John`
   - Last Name: `Doe`
   - Email: `john@test.com`
   - Phone: `+1234567890`
   - Password: `Test@1234`
     - ⚠️ Must have: uppercase, lowercase, number, special character
3. Click **"Create Account"**

🎉 **You should see the Dashboard!**

### 7.3 Verify Dashboard

You should see:
- ✅ 4 colorful stat cards (Total Expenses, Categories, etc.)
- ✅ Empty charts (no data yet - that's normal!)
- ✅ Left sidebar with menu
- ✅ Your name "John Doe" in top-right corner
- ✅ Logout button

### 7.4 Check Database

Open MySQL again:
```bash
mysql -u root -p
```

Run:
```sql
USE expense_tracker_db;
SHOW TABLES;
```

You should see these tables:
- `users`
- `categories`
- `expenses`
- `budgets`

**Check your user was created:**
```sql
SELECT id, email, first_name, last_name FROM users;
```

You should see your account!

Exit:
```sql
exit;
```

### 7.5 Check Backend API Documentation

Open new browser tab:
**http://localhost:8080/swagger-ui.html**

You should see:
- 🔷 Swagger UI interface
- 📚 All API endpoints listed
- 🔐 Authentication section
- 📊 Expenses section

---

## 🎯 STEP 8: Add Sample Data

### 8.1 Add Categories

Open MySQL:
```bash
mysql -u root -p expense_tracker_db
```

Run this:
```sql
INSERT INTO categories (name, description, icon, color, budget_limit, is_default, created_at, updated_at) VALUES
('Food & Dining', 'Restaurants and groceries', '🍔', '#ef4444', 500.00, true, NOW(), NOW()),
('Transportation', 'Fuel and transport', '🚗', '#f59e0b', 300.00, true, NOW(), NOW()),
('Shopping', 'Shopping and purchases', '🛍️', '#ec4899', 400.00, true, NOW(), NOW()),
('Entertainment', 'Movies and games', '🎮', '#8b5cf6', 200.00, true, NOW(), NOW()),
('Healthcare', 'Medical expenses', '🏥', '#10b981', 300.00, true, NOW(), NOW());
```

**Verify:**
```sql
SELECT id, name, icon FROM categories;
```

Exit:
```sql
exit;
```

### 8.2 Add Test Expense via Swagger

1. Go to: http://localhost:8080/swagger-ui.html
2. **Login first:**
   - Expand **"Authentication"**
   - Click **"POST /api/auth/login"**
   - Click **"Try it out"**
   - Enter:
     ```json
     {
       "email": "john@test.com",
       "password": "Test@1234"
     }
     ```
   - Click **"Execute"**
   - **COPY** the `accessToken` from response

3. **Authorize Swagger:**
   - Scroll to top
   - Click green **"Authorize"** button (🔓)
   - In the dialog, enter: `Bearer YOUR_ACCESS_TOKEN`
   - Click **"Authorize"**
   - Click **"Close"**

4. **Create Expense:**
   - Expand **"Expenses"**
   - Click **"POST /api/expenses"**
   - Click **"Try it out"**
   - Enter:
     ```json
     {
       "title": "Lunch at Pizza Place",
       "description": "Team lunch meeting",
       "amount": 45.50,
       "categoryId": 1,
       "expenseDate": "2024-02-13",
       "paymentMethod": "CREDIT_CARD",
       "merchant": "Pizza Palace",
       "location": "Downtown"
     }
     ```
   - Click **"Execute"**
   - Should see: **Code 201** (Created)

5. **Refresh Dashboard!**
   - Go back to: http://localhost:3000/dashboard
   - Press F5 to refresh
   - 🎉 **You should see your expense data!**

---

## 🚨 Troubleshooting

### Problem: "Port 8080 already in use"

**Find and kill the process:**

**Windows:**
```cmd
netstat -ano | findstr :8080
taskkill /PID <NUMBER> /F
```

**Mac/Linux:**
```bash
lsof -i :8080
kill -9 <PID>
```

### Problem: "Cannot connect to MySQL"

**Check MySQL is running:**

**Windows:**
```cmd
net start MySQL80
```

**Mac:**
```bash
brew services list
brew services start mysql@8.0
```

**Linux:**
```bash
sudo systemctl status mysql
sudo systemctl start mysql
```

**Test connection:**
```bash
mysql -u root -p
# Enter password: root
```

### Problem: "Access denied for user 'root'@'localhost'"

**Your password is wrong!**

Update `application.properties`:
```properties
spring.datasource.password=YOUR_ACTUAL_PASSWORD
```

Or reset MySQL root password:
```bash
# Linux/Mac
sudo mysql
ALTER USER 'root'@'localhost' IDENTIFIED BY 'root';
FLUSH PRIVILEGES;
exit;
```

### Problem: Maven build fails

**Clear cache:**
```bash
mvn clean
rm -rf ~/.m2/repository
mvn install
```

### Problem: npm install fails

**Delete and retry:**
```bash
rm -rf node_modules package-lock.json
npm cache clean --force
npm install
```

### Problem: "Unknown database 'expense_tracker_db'"

**Create it manually:**
```bash
mysql -u root -p
CREATE DATABASE expense_tracker_db;
exit;
```

---

## 📝 Quick Reference Card

### Start Application:

**Terminal 1 - Backend:**
```bash
cd smart-expense-tracker/backend
mvn spring-boot:run
```

**Terminal 2 - Frontend:**
```bash
cd smart-expense-tracker/frontend
npm run dev
```

### URLs:
- 🌐 **Frontend**: http://localhost:3000
- 🔌 **Backend**: http://localhost:8080
- 📚 **Swagger**: http://localhost:8080/swagger-ui.html
- 🗄️ **MySQL**: localhost:3306

### Stop Application:
- Press `Ctrl + C` in both terminals

### MySQL Commands:
```bash
# Login
mysql -u root -p

# Use database
USE expense_tracker_db;

# Show tables
SHOW TABLES;

# View users
SELECT * FROM users;

# View expenses
SELECT * FROM expenses;
```

---

## ✅ Success Checklist

- [ ] Java 17 installed (`java -version` works)
- [ ] Maven installed (`mvn -version` works)
- [ ] Node.js installed (`node -v` works)
- [ ] MySQL installed and running
- [ ] Database `expense_tracker_db` created
- [ ] Backend running on port 8080
- [ ] Frontend running on port 3000
- [ ] Can access login page at http://localhost:3000
- [ ] Successfully registered account
- [ ] Can see dashboard
- [ ] Swagger UI accessible
- [ ] Categories added to database
- [ ] Test expense created

---

## 🎉 Success!

If you can see your dashboard with data, **congratulations!** 🎊

You've successfully:
✅ Set up MySQL database  
✅ Configured Spring Boot backend  
✅ Connected backend to MySQL  
✅ Run React frontend  
✅ Created user account  
✅ Added expense data  
✅ Verified everything works!

This is a **production-grade application** running on your machine!

---

## 📞 Still Having Issues?

Tell me:
1. **Which step** you're stuck on
2. **Error message** (copy exact text)
3. **What you tried** so far
4. **Operating system** (Windows/Mac/Linux)

I'll help you fix it! 🚀

---

**Happy Coding!** 💻✨
