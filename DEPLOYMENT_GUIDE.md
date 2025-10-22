# 🚀 Guía de Despliegue - Astro a Azure Static Web Apps

## ✅ Preparación del Proyecto

### 1. Workflow Optimizado
- ✅ Workflow optimizado para Astro ya configurado
- ✅ Eliminados workflows antiguos innecesarios
- ✅ Configuración correcta de `output_location: "dist"`

### 2. Archivos Necesarios
```
.github/workflows/azure-static-web-apps.yml  # Workflow optimizado
package.json                                  # Dependencias de Astro
astro.config.mjs                             # Configuración de Astro
```

## 🔧 Pasos para Despliegue desde Cero

### Paso 1: Crear Static Web App en Azure
1. Ve a [Azure Portal](https://portal.azure.com)
2. Busca "Static Web Apps" y crea uno nuevo
3. Configura:
   - **Nombre**: `tu-proyecto-astro`
   - **Resource Group**: Crea uno nuevo o usa existente
   - **Plan**: Free
   - **Source**: GitHub
   - **GitHub Account**: Conecta tu cuenta
   - **Organization**: Selecciona tu organización
   - **Repository**: `Astro-Tres-Pi-Talk`
   - **Branch**: `main`

### Paso 2: Configurar GitHub Secrets
1. Ve a tu repositorio en GitHub
2. Settings → Secrets and variables → Actions
3. Agrega el secret:
   - **Name**: `AZURE_STATIC_WEB_APPS_API_TOKEN`
   - **Value**: (Copia el token que te da Azure)

### Paso 3: Configurar el Workflow
El workflow ya está optimizado, pero si necesitas cambiar el nombre del secret:
```yaml
azure_static_web_apps_api_token: ${{ secrets.AZURE_STATIC_WEB_APPS_API_TOKEN }}
```

### Paso 4: Hacer Commit y Push
```bash
git add .
git commit -m "feat: add optimized Azure deployment workflow"
git push origin main
```

## 🎯 Configuración del Workflow

### Características del Workflow Optimizado:
- ✅ **Node.js 18** configurado explícitamente
- ✅ **Cache de npm** para builds más rápidos
- ✅ **Build local** con `npm run build`
- ✅ **Skip app build** en Azure (ya está construido)
- ✅ **Output location** correcto: `dist`
- ✅ **Versiones actualizadas** de las actions

### Estructura del Workflow:
```yaml
1. Checkout del código
2. Setup de Node.js 18 con cache
3. Instalación de dependencias (npm ci)
4. Build de Astro (npm run build)
5. Deploy a Azure Static Web Apps
```

## 🐛 Solución de Problemas Comunes

### Error: "Unable to determine app artifacts location"
**Solución**: Asegúrate de que `output_location: "dist"` esté configurado

### Error: "Build failed"
**Solución**: Verifica que `package.json` tenga el script `"build": "astro build"`

### Error: "Token not found"
**Solución**: Verifica que el secret `AZURE_STATIC_WEB_APPS_API_TOKEN` esté configurado en GitHub

## 📝 Notas Importantes

1. **Solo necesitas UN workflow** - Los otros se pueden eliminar
2. **El token debe llamarse exactamente** `AZURE_STATIC_WEB_APPS_API_TOKEN`
3. **Astro genera archivos en `/dist`** - No cambiar esta configuración
4. **El workflow se ejecuta automáticamente** en cada push a `main`

## 🔄 Para Re-ejecutar Manualmente

### Opción 1: Desde GitHub
1. Ve a Actions en tu repositorio
2. Selecciona el workflow
3. Haz clic en "Re-run all jobs"

### Opción 2: Desde Azure Portal
1. Ve a tu Static Web App en Azure
2. Busca la opción "Redeploy" o "Sync"

### Opción 3: Commit vacío
```bash
git commit --allow-empty -m "trigger: re-run deployment"
git push origin main
```

## 🎉 ¡Listo!

Con esta configuración, tu proyecto Astro se desplegará automáticamente en Azure Static Web Apps cada vez que hagas push a la rama `main`.
