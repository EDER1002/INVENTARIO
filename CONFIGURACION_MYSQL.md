# Configuración para MySQL

El sistema ha sido adaptado para trabajar con MySQL. Sigue estos pasos para configurarlo:

## 1. Instalar MySQL

Si no tienes MySQL instalado, descárgalo desde: https://dev.mysql.com/downloads/mysql/

## 2. Crear la Base de Datos

Ejecuta el script SQL que proporcionaste para crear las tablas:

```sql
CREATE DATABASE inventario;
USE inventario;
-- ... (tu script SQL completo)
```

## 3. Configurar el Backend

### Instalar dependencias

```bash
cd backend
npm install
```

Esto instalará `mysql2` en lugar de `pg`.

### Crear archivo .env

Crea un archivo `.env` en la carpeta `backend`:

```env
PORT=3000
NODE_ENV=development
DB_HOST=localhost
DB_PORT=3306
DB_NAME=inventario
DB_USER=root
DB_PASSWORD=eder1002
JWT_SECRET=tu_secret_key_super_segura_aqui
JWT_EXPIRES_IN=7d
FRONTEND_URL=http://localhost:5173
```

**IMPORTANTE**: Cambia `DB_PASSWORD` por tu contraseña real (`eder1002` según indicaste).

## 4. Ejecutar Seed

Para crear el usuario admin:

```bash
cd backend
npm run seed
```

Esto creará:
- Usuario admin: `admin@inventario.com` / `admin123`
- Bodega principal
- Categorías de ejemplo
- Proveedores de ejemplo

## 5. Iniciar el Backend

```bash
npm run dev
```

## Diferencias con PostgreSQL

### Nombres de Columnas

El sistema ahora usa los nombres de tu base de datos MySQL:
- `id_usuario` en lugar de `id`
- `correo` en lugar de `email`
- `contraseña` en lugar de `password`
- `id_categoria`, `id_producto`, `id_proveedor`, etc.

### Stock

El stock se maneja en la tabla `stock` separada, no directamente en productos. El sistema calcula el stock total sumando todas las bodegas.

### Movimientos

Los movimientos usan tipos en minúsculas: `entrada`, `salida`, `ajuste` (no `ENTRADA`, `SALIDA`, etc.)

## Verificar Configuración

Ejecuta el script de verificación:

```bash
cd backend
npm run check
```

Esto te mostrará:
- Estado de la conexión
- Tablas existentes
- Usuarios registrados
- Variables de entorno

## Solución de Problemas

### Error: "Access denied for user"

Verifica que:
1. El usuario y contraseña en `.env` sean correctos
2. MySQL esté corriendo
3. El usuario tenga permisos en la base de datos `inventario`

### Error: "Table doesn't exist"

Asegúrate de haber ejecutado tu script SQL completo para crear todas las tablas.

### Error: "Cannot connect to MySQL"

Verifica que MySQL esté corriendo:
```bash
# Windows
net start MySQL80

# Linux
sudo systemctl start mysql

# macOS
brew services start mysql
```

## Estructura de Tablas Esperada

El sistema espera estas tablas:
- `usuarios`
- `categorias`
- `proveedores`
- `productos`
- `bodegas`
- `stock`
- `entradas`
- `entrada_detalle`
- `salidas`
- `salida_detalle`
- `movimientos`

¡Listo! Tu sistema está configurado para MySQL. 🎉

