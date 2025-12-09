# Sistema de Inventario Profesional

Sistema completo de gestión de inventario para empresas grandes, construido con React (frontend) y Node.js/Express/PostgreSQL (backend).

## 🚀 Características

- ✅ Gestión completa de productos, categorías y proveedores
- ✅ Control de movimientos de inventario (entradas, salidas, ajustes, devoluciones)
- ✅ Dashboard con estadísticas en tiempo real
- ✅ Reportes y análisis de rotación de productos
- ✅ Alertas de productos bajo stock
- ✅ Autenticación JWT segura
- ✅ Interfaz moderna y responsive con React
- ✅ API REST completa y documentada

## 📋 Requisitos Previos

- Node.js 18+ 
- PostgreSQL 12+
- npm o yarn

## 🛠️ Instalación

### 1. Backend

```bash
cd backend
npm install
```

### 2. Configurar Base de Datos

Crea un archivo `.env` en la carpeta `backend`:

```env
PORT=3000
NODE_ENV=development
DB_HOST=localhost
DB_PORT=5432
DB_NAME=inventario_db
DB_USER=postgres
DB_PASSWORD=tu_password
JWT_SECRET=tu_secret_key_super_segura
JWT_EXPIRES_IN=7d
FRONTEND_URL=http://localhost:5173
```

### 3. Crear Base de Datos

```sql
CREATE DATABASE inventario_db;
```

### 4. Ejecutar Migraciones

```bash
cd backend
npm run migrate
npm run seed
```

Esto creará las tablas y un usuario admin por defecto:
- Email: `admin@inventario.com`
- Password: `admin123`

### 5. Frontend

```bash
cd frontend
npm install
```

## 🚀 Ejecutar la Aplicación

### Backend (Terminal 1)

```bash
cd backend
npm run dev
```

El backend estará disponible en `http://localhost:3000`

### Frontend (Terminal 2)

```bash
cd frontend
npm run dev
```

El frontend estará disponible en `http://localhost:5173`

## 📁 Estructura del Proyecto

```
.
├── backend/
│   ├── config/
│   │   └── database.js
│   ├── controllers/
│   │   ├── auth.controller.js
│   │   ├── productos.controller.js
│   │   ├── categorias.controller.js
│   │   ├── proveedores.controller.js
│   │   ├── movimientos.controller.js
│   │   └── reportes.controller.js
│   ├── middleware/
│   │   └── auth.middleware.js
│   ├── routes/
│   │   ├── auth.routes.js
│   │   ├── productos.routes.js
│   │   ├── categorias.routes.js
│   │   ├── proveedores.routes.js
│   │   ├── movimientos.routes.js
│   │   ├── reportes.routes.js
│   │   └── usuarios.routes.js
│   ├── scripts/
│   │   ├── migrate.js
│   │   └── seed.js
│   └── server.js
│
└── frontend/
    ├── src/
    │   ├── components/
    │   │   ├── Layout.jsx
    │   │   ├── PrivateRoute.jsx
    │   │   ├── ProductoModal.jsx
    │   │   └── MovimientoModal.jsx
    │   ├── contexts/
    │   │   └── AuthContext.jsx
    │   ├── pages/
    │   │   ├── Login.jsx
    │   │   ├── Dashboard.jsx
    │   │   ├── Productos.jsx
    │   │   ├── Categorias.jsx
    │   │   ├── Proveedores.jsx
    │   │   ├── Movimientos.jsx
    │   │   └── Reportes.jsx
    │   ├── services/
    │   │   └── api.js
    │   ├── App.jsx
    │   └── main.jsx
    └── package.json
```

## 🔐 Autenticación

El sistema utiliza JWT (JSON Web Tokens) para la autenticación. Todas las rutas de la API (excepto login y register) requieren un token válido.

## 📊 API Endpoints

### Autenticación
- `POST /api/auth/register` - Registrar nuevo usuario
- `POST /api/auth/login` - Iniciar sesión
- `GET /api/auth/profile` - Obtener perfil del usuario

### Productos
- `GET /api/productos` - Listar productos (con paginación y búsqueda)
- `GET /api/productos/:id` - Obtener producto por ID
- `POST /api/productos` - Crear producto
- `PUT /api/productos/:id` - Actualizar producto
- `DELETE /api/productos/:id` - Eliminar producto

### Categorías
- `GET /api/categorias` - Listar categorías
- `GET /api/categorias/:id` - Obtener categoría por ID
- `POST /api/categorias` - Crear categoría
- `PUT /api/categorias/:id` - Actualizar categoría
- `DELETE /api/categorias/:id` - Eliminar categoría

### Proveedores
- `GET /api/proveedores` - Listar proveedores
- `GET /api/proveedores/:id` - Obtener proveedor por ID
- `POST /api/proveedores` - Crear proveedor
- `PUT /api/proveedores/:id` - Actualizar proveedor
- `DELETE /api/proveedores/:id` - Eliminar proveedor

### Movimientos
- `GET /api/movimientos` - Listar movimientos (con filtros)
- `GET /api/movimientos/:id` - Obtener movimiento por ID
- `POST /api/movimientos` - Crear movimiento
- `DELETE /api/movimientos/:id` - Eliminar movimiento (revierte stock)

### Reportes
- `GET /api/reportes/estadisticas?periodo=mes` - Estadísticas generales
- `GET /api/reportes/productos-bajo-stock` - Productos bajo stock
- `GET /api/reportes/movimientos-diarios?fecha=YYYY-MM-DD` - Movimientos del día
- `GET /api/reportes/rotacion-productos?limite=10` - Rotación de productos

## 🎨 Tecnologías Utilizadas

### Backend
- Node.js
- Express.js
- PostgreSQL
- JWT (jsonwebtoken)
- bcryptjs
- Helmet (seguridad)
- CORS

### Frontend
- React 18
- React Router
- Axios
- Recharts (gráficos)
- Tailwind CSS
- Lucide React (iconos)
- Vite

## 📝 Notas

- El sistema actualiza automáticamente el stock cuando se crean movimientos
- Los movimientos pueden revertirse, restaurando el stock anterior
- El sistema valida que no haya stock negativo en salidas
- Los productos bajo stock se muestran en el dashboard y reportes

## 🔒 Seguridad

- Contraseñas hasheadas con bcrypt
- Tokens JWT con expiración
- Middleware de autenticación en todas las rutas protegidas
- Validación de datos en el backend
- CORS configurado para el frontend

## 📄 Licencia

ISC

