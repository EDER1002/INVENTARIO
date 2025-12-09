# Guía de Instalación - Sistema de Inventario

## Paso 1: Instalar PostgreSQL

### Windows
1. Descarga PostgreSQL desde: https://www.postgresql.org/download/windows/
2. Instala PostgreSQL con las opciones por defecto
3. Anota la contraseña del usuario `postgres` que configuraste durante la instalación

### Linux (Ubuntu/Debian)
```bash
sudo apt update
sudo apt install postgresql postgresql-contrib
sudo systemctl start postgresql
sudo systemctl enable postgresql
```

### macOS
```bash
brew install postgresql
brew services start postgresql
```

## Paso 2: Crear la Base de Datos

Abre una terminal y ejecuta:

```bash
# Conectarse a PostgreSQL
psql -U postgres

# Crear la base de datos
CREATE DATABASE inventario_db;

# Salir de psql
\q
```

## Paso 3: Configurar el Backend

1. Navega a la carpeta `backend`:
```bash
cd backend
```

2. Instala las dependencias:
```bash
npm install
```

3. Crea el archivo `.env`:
```bash
# En Windows (PowerShell)
copy .env.example .env

# En Linux/macOS
cp .env.example .env
```

4. Edita el archivo `.env` y configura tus credenciales:
```env
PORT=3000
NODE_ENV=development
DB_HOST=localhost
DB_PORT=5432
DB_NAME=inventario_db
DB_USER=postgres
DB_PASSWORD=tu_password_aqui
JWT_SECRET=tu_secret_key_super_segura_cambiar_en_produccion
JWT_EXPIRES_IN=7d
FRONTEND_URL=http://localhost:5173
```

**IMPORTANTE**: Cambia `DB_PASSWORD` por la contraseña que configuraste para PostgreSQL.

## Paso 4: Ejecutar Migraciones

En la carpeta `backend`, ejecuta:

```bash
npm run migrate
```

Esto creará todas las tablas necesarias en la base de datos.

## Paso 5: Cargar Datos Iniciales

Ejecuta el script de seed para crear el usuario administrador:

```bash
npm run seed
```

Esto creará un usuario admin con:
- **Email**: `admin@inventario.com`
- **Password**: `admin123`

## Paso 6: Iniciar el Backend

```bash
npm run dev
```

El servidor estará corriendo en `http://localhost:3000`

## Paso 7: Configurar el Frontend

1. Abre una nueva terminal y navega a la carpeta `frontend`:
```bash
cd frontend
```

2. Instala las dependencias:
```bash
npm install
```

## Paso 8: Iniciar el Frontend

```bash
npm run dev
```

El frontend estará disponible en `http://localhost:5173`

## Paso 9: Acceder al Sistema

1. Abre tu navegador y ve a: `http://localhost:5173`
2. Inicia sesión con:
   - Email: `admin@inventario.com`
   - Password: `admin123`

## Solución de Problemas

### Error: "No se puede conectar a la base de datos"
- Verifica que PostgreSQL esté corriendo
- Revisa las credenciales en el archivo `.env`
- Asegúrate de que la base de datos `inventario_db` exista

### Error: "Puerto 3000 ya está en uso"
- Cambia el puerto en el archivo `.env` del backend
- O detén el proceso que está usando el puerto 3000

### Error: "Puerto 5173 ya está en uso"
- Vite automáticamente usará el siguiente puerto disponible
- O cambia el puerto en `vite.config.js`

### Error al instalar dependencias
- Asegúrate de tener Node.js 18+ instalado
- Intenta eliminar `node_modules` y `package-lock.json` y reinstalar:
```bash
rm -rf node_modules package-lock.json
npm install
```

## Comandos Útiles

### Backend
- `npm start` - Inicia el servidor en modo producción
- `npm run dev` - Inicia el servidor en modo desarrollo (con nodemon)
- `npm run migrate` - Ejecuta las migraciones de la base de datos
- `npm run seed` - Carga datos iniciales

### Frontend
- `npm run dev` - Inicia el servidor de desarrollo
- `npm run build` - Construye la aplicación para producción
- `npm run preview` - Previsualiza la build de producción

## Estructura de Archivos Importantes

```
backend/
├── .env                    # Configuración del entorno (crear desde .env.example)
├── server.js               # Punto de entrada del servidor
├── config/
│   └── database.js        # Configuración de la base de datos
└── scripts/
    ├── migrate.js         # Script de migración
    └── seed.js            # Script de datos iniciales

frontend/
├── src/
│   ├── App.jsx            # Componente principal
│   └── main.jsx          # Punto de entrada
└── vite.config.js        # Configuración de Vite
```

## Próximos Pasos

Una vez que el sistema esté funcionando:

1. Cambia la contraseña del usuario admin desde la interfaz
2. Crea categorías para organizar tus productos
3. Agrega proveedores
4. Comienza a registrar productos
5. Realiza movimientos de inventario

¡Listo! Tu sistema de inventario está funcionando. 🎉

