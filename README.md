# CAFIVER · QR Labels

App de impresión de etiquetas QR para rutas tienda-en-tienda.

## Estructura del repo

```
cafiver-repo/
├── index.html          ← App principal (GitHub Pages)
├── destnvo.csv         ← CSV de destinatarios (se actualiza automáticamente)
└── .github/
    └── workflows/
        └── sync-csv.yml  ← Sincronización nocturna desde Google Drive
```

## Setup inicial (hacer una sola vez)

### 1. Subir a GitHub

```bash
git init
git add .
git commit -m "Initial commit"
git remote add origin https://github.com/TU_USUARIO/cafiver-qr.git
git push -u origin main
```

### 2. Activar GitHub Pages

Settings → Pages → Source: **Deploy from branch** → Branch: `main` → `/root`

Tu app estará en: `https://TU_USUARIO.github.io/cafiver-qr/`

### 3. Compartir el CSV en Google Drive

1. Abre el archivo `destnvo.csv` en Google Drive
2. Clic derecho → **Compartir** → **Cualquier persona con el enlace puede ver**
3. Copia el enlace. Tiene este formato:
   `https://drive.google.com/file/d/AQUI_VA_EL_ID/view`
4. El **File ID** es la parte entre `/d/` y `/view`
   Ejemplo: `1BxiMVs0XRA5nFMdKvBdBZjgmUUqptlbs74OgVE2upms`

### 4. Guardar el File ID como Secret en GitHub

1. Ve a tu repo → **Settings** → **Secrets and variables** → **Actions**
2. Clic en **New repository secret**
3. Nombre: `GDRIVE_FILE_ID`
4. Valor: pega el ID del archivo de Drive
5. Clic en **Add secret**

### 5. Probar la sincronización manualmente

1. Ve a tu repo → pestaña **Actions**
2. Clic en **Sync CSV desde Google Drive**
3. Clic en **Run workflow** → **Run workflow**
4. Verifica que el CSV se descargó correctamente

## Horario de sincronización

Cada noche a las **22:40 hora México** (UTC-6 / CST).

Para cambiar el horario, edita `.github/workflows/sync-csv.yml`:
- El campo `cron` usa hora UTC
- 22:40 CST = 04:40 UTC → `'40 4 * * *'`
- 22:00 CST = 04:00 UTC → `'0 4 * * *'`

## Uso de la app

### Modo Individual
Escribe el número de destinatario — si el CSV está cargado, auto-completa nombre de tienda y ruta.

### Modo CSV Masivo
Filtra por **fecha de creación** para sacar todos los destinatarios de un día específico.
También puedes filtrar por ruta o nombre de tienda.
