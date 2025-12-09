# 🚀 Cómo Ejecutar el Sistema de Inventario

## Requisitos Previos

1. ✅ MySQL instalado y corriendo
2. ✅ Node.js 18+ instalado
3. ✅ Base de datos `inventario` creada con todas las tablas

## Paso 1: Configurar el Backend

### 1.1. Instalar dependencias

Abre una terminal y ejecuta:

```bash
cd backend
npm install
```

### 1.2. Crear archivo .env

Crea un archivo llamado `.env` en la carpeta `backend` con este contenido:

```env
PORT=3000
NODE_ENV=development
DB_HOST=localhost
DB_PORT=3306
DB_NAME=inventario
DB_USER=root
DB_PASSWORD=eder1002
JWT_SECRET=mi_secret_key_super_segura_123456
JWT_EXPIRES_IN=7d
FRONTEND_URL=http://localhost:5173
```

**⚠️ IMPORTANTE**: 
- Cambia `DB_PASSWORD` si tu contraseña de MySQL es diferente
- Cambia `JWT_SECRET` por una cadena aleatoria segura

### 1.3. Verificar la configuración

```bash
npm run check
```

Deberías ver:
- ✅ Conexión a base de datos: OK
- ✅ Tablas listadas
- ✅ Variables de entorno configuradas

### 1.4. Crear usuario admin (si no existe)

```bash
npm run seed
```

Esto crea:
- Usuario: `admin@inventario.com`
- Contraseña: `admin123`
- Bodega principal
- Categorías y proveedores de ejemplo

### 1.5. Iniciar el Backend

```bash
npm run dev
```

Deberías ver:
```
🚀 Servidor corriendo en puerto 3000
✅ Base de datos conectada: [timestamp]
```

**¡Mantén esta terminal abierta!**

---

## Paso 2: Configurar el Frontend

### 2.1. Abrir una NUEVA terminal

Abre otra terminal (deja la del backend corriendo).

### 2.2. Instalar dependencias

```bash
cd frontend
npm install
```

### 2.3. Iniciar el Frontend

```bash
npm run dev
```

Deberías ver algo como:
```
  VITE v5.x.x  ready in xxx ms

  ➜  Local:   http://localhost:5173/
  ➜  Network: use --host to expose
```

**¡Mantén esta terminal también abierta!**

---

## Paso 3: Acceder al Sistema

### 3.1. Abrir el navegador

Ve a: **http://localhost:5173**

### 3.2. Iniciar sesión

Usa las credenciales:
- **Email**: `admin@inventario.com`
- **Contraseña**: `admin123`

---

## 📋 Resumen de Comandos

### Terminal 1 (Backend):
```bash
cd backend
npm install
# Crear .env con tu configuración
npm run check
npm run seed
npm run dev
```

### Terminal 2 (Frontend):
```bash
cd frontend
npm install
npm run dev
```

### Navegador:
```
http://localhost:5173
```

---

## 🔧 Comandos Útiles

### Backend:
- `npm run dev` - Inicia el servidor en modo desarrollo
- `npm start` - Inicia el servidor en modo producción
- `npm run check` - Verifica la configuración
- `npm run seed` - Crea usuario admin y datos de ejemplo

### Frontend:
- `npm run dev` - Inicia el servidor de desarrollo
- `npm run build` - Construye para producción
- `npm run preview` - Previsualiza la build

---

## ⚠️ Solución de Problemas

### Error: "Cannot connect to database"
1. Verifica que MySQL esté corriendo
2. Verifica las credenciales en `.env`
3. Verifica que la base de datos `inventario` exista

### Error: "Port 3000 already in use"
- Cambia el puerto en `.env`: `PORT=3001`
- O cierra el proceso que usa el puerto 3000

### Error: "Port 5173 already in use"
- Vite automáticamente usará el siguiente puerto disponible
- O cambia el puerto en `vite.config.js`

### No puedo iniciar sesión
1. Verifica que el backend esté corriendo (puerto 3000)
2. Verifica que hayas ejecutado `npm run seed`
3. Verifica las credenciales: `admin@inventario.com` / `admin123`

### Error al instalar dependencias
```bash
# Elimina node_modules y reinstala
rm -rf node_modules package-lock.json
npm install
```

---

## ✅ Verificación Rápida

1. **Backend corriendo?**
   - Abre: http://localhost:3000/health
   - Deberías ver: `{"status":"ok",...}`

2. **Frontend corriendo?**
   - Abre: http://localhost:5173
   - Deberías ver la pantalla de login

3. **Base de datos conectada?**
   - Ejecuta: `cd backend && npm run check`
   - Deberías ver: ✅ Conexión a base de datos: OK

---

## 🎉 ¡Listo!

Si todo está bien, deberías poder:
- ✅ Ver la pantalla de login
- ✅ Iniciar sesión con `admin@inventario.com` / `admin123`
- ✅ Ver el dashboard
- ✅ Gestionar productos, categorías, proveedores, etc.

**¡Disfruta tu sistema de inventario!** 🚀

