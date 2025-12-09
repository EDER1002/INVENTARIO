# Solución: Error ECONNREFUSED

## 🔴 Problema

El error `ECONNREFUSED` significa que el **backend no está corriendo**. El frontend intenta conectarse a `http://localhost:3000` pero no encuentra el servidor.

## ✅ Solución

### Paso 1: Iniciar el Backend PRIMERO

Abre una **nueva terminal de PowerShell** y ejecuta:

```powershell
# Ir a la carpeta backend
cd C:\Users\DELL\Documents\TRABAJO\INVENTARIO\backend

# Verificar que el archivo .env existe
# Si no existe, créalo con tu configuración de MySQL

# Verificar configuración
npm run check

# Crear usuario admin (si no lo has hecho)
npm run seed

# INICIAR EL BACKEND
npm run dev
```

**Espera a ver este mensaje:**
```
🚀 Servidor corriendo en puerto 3000
✅ Base de datos conectada: [timestamp]
```

### Paso 2: Luego iniciar el Frontend

En la terminal donde tienes el frontend:

```powershell
# Asegúrate de estar en la carpeta frontend
cd C:\Users\DELL\Documents\TRABAJO\INVENTARIO\frontend

# Iniciar el frontend
npm run dev
```

## 📋 Orden Correcto

1. ✅ **PRIMERO**: Backend corriendo en puerto 3000
2. ✅ **DESPUÉS**: Frontend corriendo en puerto 5173
3. ✅ **FINALMENTE**: Abrir navegador en http://localhost:5173

## 🔍 Verificar que el Backend está Corriendo

Abre tu navegador y ve a:
```
http://localhost:3000/health
```

Deberías ver:
```json
{"status":"ok","timestamp":"..."}
```

Si ves esto, el backend está funcionando correctamente.

## ⚠️ Si el Backend No Inicia

### Error: "Cannot connect to database"
1. Verifica que MySQL esté corriendo
2. Verifica el archivo `.env` en la carpeta `backend`
3. Verifica que la contraseña sea correcta: `eder1002`

### Error: "Port 3000 already in use"
Algo más está usando el puerto 3000. Puedes:
- Cerrar el otro proceso
- O cambiar el puerto en `.env`: `PORT=3001`

## 🎯 Resumen

**El backend DEBE estar corriendo antes que el frontend.**

```
Terminal 1: Backend (npm run dev) → Puerto 3000 ✅
Terminal 2: Frontend (npm run dev) → Puerto 5173 ✅
Navegador: http://localhost:5173 ✅
```

