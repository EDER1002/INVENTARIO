# Solución de Problemas - Sistema de Inventario

## Error: "Error al iniciar sesión" o "No se pudo conectar con el servidor"

### Paso 1: Verificar que el Backend esté Corriendo

Abre una terminal y ejecuta:

```bash
cd backend
npm run dev
```

Deberías ver:
```
🚀 Servidor corriendo en puerto 3000
✅ Base de datos conectada: [timestamp]
```

Si ves un error, continúa con los siguientes pasos.

### Paso 2: Verificar la Configuración

Ejecuta el script de verificación:

```bash
cd backend
npm run check
```

Este script te dirá:
- Si la base de datos está conectada
- Qué tablas existen
- Si hay usuarios creados
- Si las variables de entorno están configuradas

### Paso 3: Verificar el Archivo .env

Asegúrate de que el archivo `backend/.env` existe y tiene el contenido correcto:

```env
PORT=3000
NODE_ENV=development
DB_HOST=localhost
DB_PORT=5432
DB_NAME=inventario_db
DB_USER=postgres
DB_PASSWORD=tu_password_aqui
JWT_SECRET=tu_secret_key_super_segura
JWT_EXPIRES_IN=7d
FRONTEND_URL=http://localhost:5173
```

**IMPORTANTE**: 
- Cambia `DB_PASSWORD` por tu contraseña real de PostgreSQL
- Cambia `JWT_SECRET` por una cadena aleatoria segura (puedes usar: `openssl rand -base64 32`)

### Paso 4: Verificar que PostgreSQL esté Corriendo

**Windows:**
```bash
# Verificar si el servicio está corriendo
Get-Service postgresql*

# O iniciar el servicio
Start-Service postgresql-x64-14  # Ajusta la versión según tu instalación
```

**Linux/macOS:**
```bash
# Verificar estado
sudo systemctl status postgresql

# Iniciar si no está corriendo
sudo systemctl start postgresql
```

### Paso 5: Verificar que la Base de Datos Exista

Conecta a PostgreSQL:

```bash
psql -U postgres
```

Luego ejecuta:

```sql
\l  -- Listar bases de datos
```

Si no existe `inventario_db`, créala:

```sql
CREATE DATABASE inventario_db;
\q
```

### Paso 6: Ejecutar Migraciones

```bash
cd backend
npm run migrate
```

Deberías ver:
```
✅ Tablas creadas exitosamente
✅ Migración completada
```

### Paso 7: Cargar Usuario Admin

```bash
cd backend
npm run seed
```

Deberías ver:
```
✅ Usuario admin creado (email: admin@inventario.com, password: admin123)
✅ Seed completado exitosamente
```

### Paso 8: Verificar que el Frontend Pueda Conectarse

Abre el navegador y ve a: `http://localhost:3000/health`

Deberías ver:
```json
{"status":"ok","timestamp":"..."}
```

Si no ves esto, el backend no está corriendo correctamente.

### Paso 9: Verificar el Proxy de Vite

El archivo `frontend/vite.config.js` debe tener:

```js
proxy: {
  '/api': {
    target: 'http://localhost:3000',
    changeOrigin: true
  }
}
```

### Paso 10: Verificar la Consola del Navegador

Abre las herramientas de desarrollador (F12) y ve a la pestaña "Console" y "Network". 

- **Console**: Busca errores en rojo
- **Network**: Cuando intentes hacer login, busca la petición a `/api/auth/login` y verifica:
  - Status code (debería ser 200)
  - Response (debería tener `success: true`)

## Errores Comunes y Soluciones

### Error: "Cannot connect to database"

**Causa**: PostgreSQL no está corriendo o las credenciales son incorrectas.

**Solución**:
1. Verifica que PostgreSQL esté corriendo
2. Verifica las credenciales en `.env`
3. Verifica que la base de datos exista

### Error: "relation 'usuarios' does not exist"

**Causa**: Las tablas no se han creado.

**Solución**:
```bash
cd backend
npm run migrate
```

### Error: "Credenciales inválidas"

**Causa**: El usuario no existe o la contraseña es incorrecta.

**Solución**:
```bash
cd backend
npm run seed
```

Esto creará el usuario:
- Email: `admin@inventario.com`
- Password: `admin123`

### Error: "Network Error" o "Failed to fetch"

**Causa**: El backend no está corriendo o hay un problema de CORS.

**Solución**:
1. Verifica que el backend esté corriendo en el puerto 3000
2. Verifica que `FRONTEND_URL` en `.env` sea `http://localhost:5173`
3. Reinicia el backend después de cambiar `.env`

### Error: "JWT_SECRET is not defined"

**Causa**: La variable de entorno JWT_SECRET no está configurada.

**Solución**:
Agrega en `backend/.env`:
```env
JWT_SECRET=tu_secret_key_super_segura_aqui
```

### Error: "Port 3000 is already in use"

**Causa**: Otro proceso está usando el puerto 3000.

**Solución**:

**Windows:**
```powershell
# Encontrar el proceso
netstat -ano | findstr :3000

# Matar el proceso (reemplaza PID con el número que aparezca)
taskkill /PID [PID] /F
```

**Linux/macOS:**
```bash
# Encontrar el proceso
lsof -i :3000

# Matar el proceso
kill -9 [PID]
```

O cambia el puerto en `backend/.env`:
```env
PORT=3001
```

Y actualiza `frontend/vite.config.js`:
```js
proxy: {
  '/api': {
    target: 'http://localhost:3001',
    changeOrigin: true
  }
}
```

## Verificación Rápida

Ejecuta estos comandos en orden:

```bash
# 1. Verificar configuración
cd backend
npm run check

# 2. Si faltan tablas, crear migraciones
npm run migrate

# 3. Si no hay usuarios, cargar seed
npm run seed

# 4. Iniciar backend
npm run dev

# 5. En otra terminal, iniciar frontend
cd frontend
npm run dev
```

## Contacto y Soporte

Si después de seguir estos pasos aún tienes problemas:

1. Revisa los logs del backend en la terminal
2. Revisa la consola del navegador (F12)
3. Verifica que todas las dependencias estén instaladas:
   ```bash
   cd backend && npm install
   cd ../frontend && npm install
   ```

