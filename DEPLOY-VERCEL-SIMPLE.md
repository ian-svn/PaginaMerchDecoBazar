# 🚀 Deploy en Vercel - Guía Simplificada

## ⚡ Pasos Rápidos

### 1. Preparar Base de Datos (PlanetScale)

1. Ve a https://planetscale.com y crea cuenta
2. Crea una base de datos
3. Copia las credenciales de conexión

### 2. Subir a GitHub

```bash
git init
git add .
git commit -m "Initial commit"
git remote add origin [URL_DE_TU_REPO]
git push -u origin main
```

### 3. Deploy en Vercel

1. Ve a https://vercel.com
2. "New Project" → Importa tu repo de GitHub
3. **Configuración:**
   - Framework: Other
   - Root Directory: `./`
   - Build Command: `npm run build`
   - Output Directory: `client/build`
   - Install Command: `npm install && cd client && npm install`

4. **Variables de Entorno:**
   ```
   DB_HOST=tu-host-planetscale
   DB_USER=tu-usuario
   DB_PASSWORD=tu-password
   DB_NAME=tu-base-de-datos
   DB_PORT=3306
   JWT_SECRET=tu-secreto-super-seguro
   NODE_ENV=production
   CLIENT_URL=https://tu-proyecto.vercel.app
   ```

5. **Deploy** → ¡Listo!

### 4. Inicializar Base de Datos

Después del deploy, ejecuta localmente:
```bash
# Actualiza .env con credenciales de PlanetScale
node server/scripts/init-db.js
```

## ✅ Listo

Tu app estará en: `https://tu-proyecto.vercel.app`

