# 💰 Smart Expense Tracker - AI-Powered Finance Management

A full-stack expense tracking application built with **Spring Boot**, **React**, **PostgreSQL**, and **JWT Authentication**. Features AI-powered insights, real-time analytics, and modern UI/UX.

[![Java](https://img.shields.io/badge/Java-17-orange.svg)](https://www.oracle.com/java/)
[![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.2.0-brightgreen.svg)](https://spring.io/projects/spring-boot)
[![React](https://img.shields.io/badge/React-18.2-blue.svg)](https://reactjs.org/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-15-blue.svg)](https://www.postgresql.org/)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

## 🚀 Features

### Core Features
- ✅ **User Authentication & Authorization** - JWT-based secure authentication with Spring Security
- ✅ **Expense Management** - Full CRUD operations for expenses with categorization
- ✅ **Real-time Dashboard** - Interactive charts and statistics using Recharts
- ✅ **Category-based Tracking** - Organize expenses by customizable categories
- ✅ **Date Range Filtering** - Filter and analyze expenses by custom date ranges
- ✅ **Budget Management** - Set and track budgets by category
- ✅ **Payment Methods** - Track expenses across multiple payment methods (Cash, Card, UPI, etc.)
- ✅ **Responsive Design** - Mobile-first design with Tailwind CSS

### Advanced Features (Architecture Ready)
- 🔄 **Recurring Expenses** - Support for recurring transactions
- 📊 **Advanced Analytics** - Category-wise breakdowns and trends
- 💱 **Multi-currency Support** - Track expenses in different currencies
- 📄 **Export Capabilities** - Export reports to PDF/Excel (backend ready)
- 📸 **Receipt Scanning** - OCR support for receipt data extraction (backend ready)
- 🔔 **Budget Alerts** - Get notified when approaching budget limits

## 🏗️ Tech Stack

### Backend
- **Java 17** - Programming language
- **Spring Boot 3.2** - Application framework
- **Spring Security** - Authentication & authorization
- **Spring Data JPA** - Database ORM
- **MySQL 8.0** - Primary database (PostgreSQL also supported)
- **JWT** - Token-based authentication
- **Maven** - Dependency management
- **Swagger/OpenAPI** - API documentation
- **Lombok** - Boilerplate code reduction

### Frontend
- **React 18** - UI library
- **Vite** - Build tool & dev server
- **Tailwind CSS** - Utility-first CSS framework
- **React Router** - Client-side routing
- **Axios** - HTTP client
- **Recharts** - Data visualization
- **React Hot Toast** - Toast notifications
- **Lucide React** - Icon library
- **date-fns** - Date manipulation

### DevOps & Tools
- **Docker** - Containerization
- **Docker Compose** - Multi-container orchestration
- **Git** - Version control
- **PostgreSQL** - Production database

## 📁 Project Structure

```
smart-expense-tracker/
├── backend/                    # Spring Boot Application
│   ├── src/
│   │   ├── main/
│   │   │   ├── java/com/expensetracker/
│   │   │   │   ├── config/           # Security & App configurations
│   │   │   │   ├── controller/       # REST API endpoints
│   │   │   │   ├── dto/              # Data Transfer Objects
│   │   │   │   ├── entity/           # JPA Entities
│   │   │   │   ├── repository/       # Data access layer
│   │   │   │   ├── service/          # Business logic
│   │   │   │   ├── security/         # JWT & Security components
│   │   │   │   ├── exception/        # Custom exceptions
│   │   │   │   └── util/             # Utility classes
│   │   │   └── resources/
│   │   │       └── application.properties
│   │   └── test/                     # Unit & Integration tests
│   ├── pom.xml                       # Maven dependencies
│   └── Dockerfile
│
├── frontend/                   # React Application
│   ├── src/
│   │   ├── components/              # Reusable UI components
│   │   ├── pages/                   # Page components
│   │   ├── services/                # API service layer
│   │   ├── contexts/                # React Context (Auth, etc.)
│   │   ├── utils/                   # Utility functions
│   │   ├── assets/                  # Static assets
│   │   ├── App.jsx                  # Main app component
│   │   ├── main.jsx                 # Entry point
│   │   └── index.css                # Global styles
│   ├── package.json
│   ├── vite.config.js
│   ├── tailwind.config.js
│   └── Dockerfile
│
├── docker-compose.yml          # Multi-container setup
├── .gitignore
└── README.md
```

## 🛠️ Installation & Setup

### Prerequisites
- Java 17 or higher
- Node.js 18 or higher
- MySQL 8.0 or higher (PostgreSQL also supported)
- Maven 3.9 or higher
- Docker & Docker Compose (optional)

> **📌 Using MySQL?** See **[MYSQL_SETUP_GUIDE.md](MYSQL_SETUP_GUIDE.md)** for complete MySQL setup instructions!

### Option 1: Manual Setup

#### 1. Clone the Repository
```bash
git clone https://github.com/yourusername/smart-expense-tracker.git
cd smart-expense-tracker
```

#### 2. Setup MySQL Database
```sql
CREATE DATABASE expense_tracker_db;
```

For detailed MySQL setup instructions, see **[MYSQL_SETUP_GUIDE.md](MYSQL_SETUP_GUIDE.md)**

#### 3. Configure Backend
```bash
cd backend
```

Update `src/main/resources/application.properties`:
```properties
# MySQL Configuration
spring.datasource.url=jdbc:mysql://localhost:3306/expense_tracker_db?createDatabaseIfNotExist=true&useSSL=false&allowPublicKeyRetrieval=true&serverTimezone=UTC
spring.datasource.username=root
spring.datasource.password=your_password

# JWT Secret (generate your own)
jwt.secret=your-secret-key-here
```

#### 4. Run Backend
```bash
mvn clean install
mvn spring-boot:run
```
Backend will start on **http://localhost:8080**

#### 5. Setup Frontend
```bash
cd ../frontend
npm install
npm run dev
```
Frontend will start on **http://localhost:3000**

### Option 2: Docker Setup (Recommended)

```bash
# From project root
docker-compose up --build

# Access the application
# Frontend: http://localhost:3000
# Backend: http://localhost:8080
# Database: localhost:5432
```

## 📚 API Documentation

Once the backend is running, access Swagger UI:
```
http://localhost:8080/swagger-ui.html
```

### Key Endpoints

#### Authentication
- `POST /api/auth/register` - Register new user
- `POST /api/auth/login` - Login user

#### Expenses
- `GET /api/expenses` - Get all expenses (paginated)
- `GET /api/expenses/{id}` - Get expense by ID
- `POST /api/expenses` - Create new expense
- `PUT /api/expenses/{id}` - Update expense
- `DELETE /api/expenses/{id}` - Delete expense
- `GET /api/expenses/filter` - Filter expenses
- `GET /api/expenses/stats` - Get expense statistics

## 🔐 Security

- **JWT Authentication** - Stateless authentication using JSON Web Tokens
- **BCrypt Password Hashing** - Secure password storage
- **Role-based Access Control** - USER and ADMIN roles
- **CORS Configuration** - Cross-origin resource sharing enabled
- **Input Validation** - Server-side validation using Bean Validation
- **SQL Injection Prevention** - Parameterized queries with JPA

## 🎨 Screenshots

### Dashboard
![Dashboard](screenshots/dashboard.png)

### Expense Management
![Expenses](screenshots/expenses.png)

### Analytics
![Analytics](screenshots/analytics.png)

## 🧪 Testing

### Backend Tests
```bash
cd backend
mvn test
```

### Frontend Tests
```bash
cd frontend
npm test
```

## 📦 Deployment

### Backend Deployment (Heroku/Railway/Render)
```bash
# Build JAR
cd backend
mvn clean package -DskipTests

# Deploy JAR file to your platform
```

### Frontend Deployment (Vercel/Netlify)
```bash
cd frontend
npm run build

# Deploy dist/ folder to your platform
```

### Docker Deployment
```bash
docker-compose -f docker-compose.prod.yml up -d
```

## 🚧 Future Enhancements

- [ ] AI-powered spending predictions
- [ ] Budget recommendations using ML
- [ ] Receipt OCR integration
- [ ] Email notifications
- [ ] Mobile app (React Native)
- [ ] Social sharing features
- [ ] Bill splitting functionality
- [ ] Investment tracking
- [ ] Tax calculation helpers
- [ ] Multiple language support

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 👨‍💻 Author

**Priyanka Konnur**
- GitHub: [@priyankakonnur](https://github.com/priyankakonnur)
- LinkedIn: [priyanka-konnur](https://linkedin.com/in/priyanka-konnur)
- Email: konnurpriyanka710@gmail.com

## 🙏 Acknowledgments

- Spring Boot Team for the amazing framework
- React Team for the UI library
- Tailwind CSS for the styling framework
- Recharts for data visualization components
- All open-source contributors

## 📞 Support

For support, email konnurpriyanka710@gmail.com or open an issue in the repository.

---

⭐ **Star this repo if you find it helpful!** ⭐
