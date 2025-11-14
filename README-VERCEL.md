# 🚀 Deploy en Vercel - Guía Completa

## ⚠️ IMPORTANTE: Configuración para Vercel

Este proyecto está configurado para funcionar en Vercel. Las imágenes están en `client/public/assets/` para que se incluyan en el build de React.

## 📋 Pasos para Deploy

### 1. Preparar Base de Datos

Necesitas una base de datos MySQL en la nube. Opciones:
- **PlanetScale** (recomendado): https://planetscale.com
- **Railway**: https://railway.app
- **Aiven**: https://aiven.io

### 2. Subir a GitHub

```bash
git init
git add .
git commit -m "Initial commit"
git remote add origin [URL_DE_TU_REPO]
git push -u origin main
```

### 3. Deploy en Vercel

1. Ve a https://vercel.com y crea una cuenta
2. Click en **"New Project"**
3. Importa tu repositorio de GitHub
4. **Configuración del proyecto:**
   - Framework Preset: **Other**
   - Root Directory: `./` (raíz del proyecto)
   - Build Command: `npm run vercel-build`
   - Output Directory: `client/build`
   - Install Command: `npm install`
   
   **NOTA:** Vercel detectará automáticamente la función serverless en `api/index.js`. No necesitas configurar nada adicional en las funciones.

5. **Variables de Entorno** (Settings → Environment Variables):
   ```
   DB_HOST=tu-host-mysql
   DB_USER=tu-usuario
   DB_PASSWORD=tu-password
   DB_NAME=tu-base-de-datos
   DB_PORT=3306
   JWT_SECRET=tu-secreto-super-seguro-cambiar-en-produccion
   NODE_ENV=production
   CLIENT_URL=https://tu-proyecto.vercel.app
   ```

6. Click en **"Deploy"**

### 4. Inicializar Base de Datos

Después del deploy, ejecuta localmente para inicializar la base de datos:

```bash
# 1. Actualiza tu .env con las credenciales de tu base de datos MySQL
# 2. Ejecuta:
node server/scripts/init-db.js
```

Esto creará:
- Las tablas necesarias
- Usuario admin: `admin` / `admin123`
- Productos de ejemplo con imágenes

### 5. Verificar

1. Visita tu URL de Vercel: `https://tu-proyecto.vercel.app`
2. Verifica que las imágenes carguen: `/assets/Logo.png`
3. Prueba el login admin: `admin` / `admin123`

## 🔧 Estructura para Vercel

```
/
├── api/
│   └── index.js          # Serverless function para Vercel
├── client/
│   ├── public/
│   │   └── assets/       # Imágenes (se incluyen en build)
│   └── src/              # Código React
├── server/               # Código del servidor (usado por api/index.js)
├── vercel.json           # Configuración de Vercel
└── package.json
```

## ✅ Características

- ✅ Imágenes servidas desde `client/public/assets/`
- ✅ API como serverless function en `/api`
- ✅ Rutas de React funcionando correctamente
- ✅ Variables de entorno configuradas

## 🐛 Solución de Problemas

### Las imágenes no cargan
- Verifica que las imágenes estén en `client/public/assets/`
- Las rutas deben ser `/assets/nombre-imagen.png` (con `/` al inicio)

### La API no funciona
- Verifica las variables de entorno en Vercel
- Revisa los logs en Vercel Dashboard → Deployments → Functions

### Error de base de datos
- Verifica que la base de datos MySQL esté accesible desde internet
- Revisa las credenciales en las variables de entorno

## 📝 Notas

- Las imágenes están en `client/public/assets/` para que React las incluya en el build
- El API está en `api/index.js` como serverless function
- Las rutas `/api/*` se redirigen automáticamente a la función serverless

