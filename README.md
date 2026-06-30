# CRUD Project - React + Spring Boot + Oracle

یک پروژه CRUD کامل با:
- **Frontend**: React + TypeScript (Function Based) + Pure CSS + Axios
- **Backend**: Java Spring Boot + Configuration Properties
- **Database**: Oracle 26 AI
- **Logging**: SLF4J Logger برای هر عملیات

## ساختار پروژه

```
crud-project/
├── frontend/
│   ├── src/
│   │   ├── components/
│   │   ├── services/
│   │   ├── styles/
│   │   └── App.tsx
│   └── package.json
└── backend/
    ├── src/main/java/com/crud/
    ├── src/main/resources/
    └── pom.xml
```

## نحوه اجرا

### Backend
```bash
cd backend
mvn clean install
mvn spring-boot:run
```

### Frontend
```bash
cd frontend
npm install
npm start
```

## توضیحات

- هر رفرش صفحه Reload Logger فراخوانی می‌شود
- هر ایجاد، حذف و ویرایش رکورد لاگ شامل JSON داده‌ها
