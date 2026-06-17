# Setup Guide - CRUD Project

## Prerequisites

- **Java 21** - [Download](https://www.oracle.com/java/technologies/downloads/#java21)
- **Maven 3.8+** - [Download](https://maven.apache.org/download.cgi)
- **Node.js 18+** - [Download](https://nodejs.org/)
- **Oracle 26 AI** - Database instance setup

## Database Setup (Oracle)

### 1. Create Database User

```sql
CREATE USER crud_user IDENTIFIED BY crud_password;
GRANT CONNECT, RESOURCE TO crud_user;
GRANT UNLIMITED TABLESPACE TO crud_user;
```

### 2. Create Connection String

```
jdbc:oracle:thin:@localhost:1521:XE
Username: crud_user
Password: crud_password
```

## Backend Setup

### 1. Navigate to Backend Directory

```bash
cd backend
```

### 2. Update Database Configuration

Edit `src/main/resources/application.yml`:

```yaml
spring:
  datasource:
    url: jdbc:oracle:thin:@YOUR_HOST:1521:YOUR_SID
    username: crud_user
    password: crud_password
```

### 3. Install Dependencies & Run

```bash
# Install dependencies
mvn clean install

# Run Spring Boot application
mvn spring-boot:run
```

The backend will start on `http://localhost:8080/api`

### 4. API Endpoints

- **GET** `/api/products` - Get all products
- **GET** `/api/products/{id}` - Get product by ID
- **POST** `/api/products` - Create new product
- **PUT** `/api/products/{id}` - Update product
- **DELETE** `/api/products/{id}` - Delete product
- **GET** `/api/products/search/by-name?name=value` - Search by name
- **GET** `/api/products/stock/low?threshold=10` - Get low stock products

## Frontend Setup

### 1. Navigate to Frontend Directory

```bash
cd frontend
```

### 2. Install Dependencies

```bash
npm install
```

### 3. Configure API URL

Edit `.env`:

```
REACT_APP_API_URL=http://localhost:8080/api
```

### 4. Start Development Server

```bash
npm start
```

The frontend will open on `http://localhost:3000`

## Project Structure

```
crud-project/
├── backend/
│   ├── src/
│   │   ├── main/
│   │   │   ├── java/com/crud/
│   │   │   │   ├── controller/      # REST Controllers
│   │   │   │   ├── service/         # Business Logic
│   │   │   │   ├── repository/      # Data Access
│   │   │   │   ├── entity/          # JPA Entities
│   │   │   │   ├── dto/             # Data Transfer Objects
│   │   │   │   ├── exception/       # Exception Handlers
│   │   │   │   ├── config/          # Configuration Classes
│   │   │   │   └── CrudApplication.java
│   │   │   └── resources/
│   │   │       ├── application.yml  # Configuration
│   │   │       └── data.sql         # Sample Data
│   │   └── test/
│   └── pom.xml                      # Maven Configuration
│
├── frontend/
│   ├── src/
│   │   ├── components/              # React Class Components
│   │   │   ├── ProductForm.tsx
│   │   │   └── ProductList.tsx
│   │   ├── services/                # API Services
│   │   │   └── api.ts
│   │   ├── types/                   # TypeScript Interfaces
│   │   │   └── Product.ts
│   │   ├── styles/                  # CSS Styles
│   │   │   └── index.css
│   │   ├── App.tsx                  # Main App Component
│   │   └── index.tsx                # Entry Point
│   ├── public/
│   │   └── index.html
│   ├── .env                         # Environment Variables
│   ├── package.json
│   ├── tsconfig.json
│   └── README.md
│
├── README.md
├── SETUP.md
└── .gitignore
```

## Features

### Frontend
- ✅ React 18+ with Class-based Components
- ✅ TypeScript for type safety
- ✅ Axios for API communication
- ✅ Pure CSS styling (no frameworks)
- ✅ CRUD operations (Create, Read, Update, Delete)
- ✅ Search functionality
- ✅ Low stock filter
- ✅ Responsive design

### Backend
- ✅ Spring Boot 4.1.0
- ✅ Java 21
- ✅ JPA/Hibernate ORM
- ✅ Oracle database integration
- ✅ RESTful API
- ✅ Global exception handling
- ✅ CORS configuration
- ✅ Logging with SLF4J

### Database
- ✅ Oracle 26 AI
- ✅ Product entity with full CRUD
- ✅ Custom queries
- ✅ Soft delete (isActive flag)
- ✅ Timestamps (createdAt, updatedAt)

## Docker Support (Optional)

### Build Backend Image

```bash
cd backend
mvn clean package
docker build -t crud-backend .
docker run -p 8080:8080 crud-backend
```

### Build Frontend Image

```bash
cd frontend
npm run build
docker build -t crud-frontend .
docker run -p 3000:3000 crud-frontend
```

## Troubleshooting

### Backend Issues

**Issue**: Cannot connect to Oracle database
- Check Oracle is running and accessible
- Verify database URL, username, and password
- Ensure Oracle JDBC driver is in classpath

**Issue**: Port 8080 already in use
```bash
# Change port in application.yml
server:
  port: 8081
```

### Frontend Issues

**Issue**: Cannot connect to API
- Verify backend is running on http://localhost:8080/api
- Check REACT_APP_API_URL in .env
- Check browser console for CORS errors

**Issue**: Port 3000 already in use
```bash
PORT=3001 npm start
```

## Testing the Application

### Create Product
1. Click "Add New Product"
2. Fill in product details
3. Click "Create Product"

### Read Products
1. View all products in the list
2. Click "Edit" to view details

### Update Product
1. Click "Edit" on any product
2. Modify details
3. Click "Update Product"

### Delete Product
1. Click "Delete" on any product
2. Confirm deletion

### Search
1. Use search box to find products by name
2. Click "Low Stock" to filter products with low inventory

## Performance Tips

- Backend uses lazy loading for relationships
- Frontend implements pagination ready (can add easily)
- Database indexes on frequently queried fields
- CORS optimized for production

## Security Considerations

- Validate all inputs on both frontend and backend
- Use HTTPS in production
- Implement authentication/authorization
- Use environment variables for sensitive data
- Sanitize user inputs

## Next Steps

1. Add authentication (JWT/OAuth)
2. Implement pagination
3. Add unit tests
4. Setup CI/CD pipeline
5. Deploy to production
