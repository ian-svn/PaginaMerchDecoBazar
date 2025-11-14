# 🗄️ Inicializar Base de Datos en Vercel

## ⚠️ Problema

Si ves un error 404 o no aparecen productos, probablemente la base de datos no está inicializada.

## ✅ Solución Rápida

### Opción 1: Usar el Endpoint de Inicialización (Recomendado)

1. **Configura una variable de entorno en Vercel:**
   - Ve a tu proyecto en Vercel
   - Settings → Environment Variables
   - Añade: `INIT_DB_SECRET` = `tu_secreto_super_seguro_2024`
   - Guarda y haz un nuevo deploy

2. **Inicializa la base de datos:**
   - Visita: `https://tu-proyecto.vercel.app/api/init-db?secret=tu_secreto_super_seguro_2024`
   - O usa curl:
     ```bash
     curl "https://tu-proyecto.vercel.app/api/init-db?secret=tu_secreto_super_seguro_2024"
     ```

3. **Verifica:**
   - Deberías ver un mensaje de éxito
   - Ahora prueba el login: `admin` / `admin123`
   - Los productos deberían aparecer

### Opción 2: Inicializar Localmente

1. **Configura tu `.env` local con las credenciales de tu base de datos MySQL en la nube:**
   ```env
   DB_HOST=tu-host-mysql
   DB_USER=tu-usuario
   DB_PASSWORD=tu-password
   DB_NAME=tu-base-de-datos
   DB_PORT=3306
   ```

2. **Ejecuta el script de inicialización:**
   ```bash
   node server/scripts/init-db.js
   ```

3. **Verifica en Vercel:**
   - Recarga tu aplicación
   - Prueba el login: `admin` / `admin123`

## 🔍 Verificar que la API Funciona

1. **Prueba el endpoint de test:**
   - Visita: `https://tu-proyecto.vercel.app/api/test`
   - Deberías ver: `{"message":"API funcionando correctamente en Vercel"}`

2. **Si el test funciona pero el login no:**
   - La base de datos no está inicializada
   - Sigue los pasos de inicialización arriba

3. **Si el test NO funciona (404):**
   - Verifica que las variables de entorno estén configuradas
   - Revisa los logs en Vercel Dashboard → Deployments → Functions
   - Verifica que `api/index.js` esté en la raíz del proyecto

## 📋 Checklist de Variables de Entorno en Vercel

Asegúrate de tener estas variables configuradas:

```
DB_HOST=tu-host-mysql
DB_USER=tu-usuario
DB_PASSWORD=tu-password
DB_NAME=tu-base-de-datos
DB_PORT=3306
JWT_SECRET=tu-secreto-super-seguro
NODE_ENV=production
CLIENT_URL=https://tu-proyecto.vercel.app
INIT_DB_SECRET=tu_secreto_super_seguro_2024 (opcional, para proteger el endpoint)
```

## 🐛 Solución de Problemas

### Error 404 en /api/test
- Verifica que `api/index.js` exista
- Verifica que `vercel.json` esté configurado correctamente
- Revisa los logs de deploy en Vercel

### Error de conexión a base de datos
- Verifica que las credenciales sean correctas
- Verifica que la base de datos MySQL esté accesible desde internet
- Algunos proveedores requieren whitelist de IPs (Vercel usa IPs dinámicas)

### La base de datos se inicializa pero no aparecen productos
- Verifica que las imágenes estén en `client/public/assets/`
- Revisa la consola del navegador para errores
- Verifica que las rutas de imágenes en la BD sean `/assets/nombre-imagen.png`

## 🔐 Seguridad

**IMPORTANTE:** Después de inicializar la base de datos, considera:
1. Eliminar o deshabilitar el endpoint `/api/init-db`
2. Cambiar la contraseña del admin desde el panel
3. Usar un secreto fuerte para `INIT_DB_SECRET`

