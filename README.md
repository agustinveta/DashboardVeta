# Veta Agency — Dashboard Financiero

Dashboard financiero interno con datos reales 2024–2025–2026, alimentado por Google Sheets.

---

## Setup paso a paso

### 1. Publicar el Google Sheet

1. Abrí el archivo en Google Drive: https://docs.google.com/spreadsheets/d/1ThZvjoiw2J8-mSoPnvfYJyh9kHl2S3Rs
2. Menú **Archivo → Compartir → Publicar en la web**
3. En "Hoja" elegí la pestaña que contiene los datos mensuales
4. Formato: **Página web**
5. Hacé clic en **Publicar**
6. Aceptá la confirmación

> El sheet sigue siendo privado para edición — solo los datos se publican en modo lectura para la API de gviz.

---

### 2. Obtener el Sheet ID

El Sheet ID ya está en la URL del sheet:

```
https://docs.google.com/spreadsheets/d/1ThZvjoiw2J8-mSoPnvfYJyh9kHl2S3Rs/edit...
                                        ↑ este es el ID
```

Para este proyecto: `1ThZvjoiw2J8-mSoPnvfYJyh9kHl2S3Rs`

---

### 3. Configurar el dashboard

Abrí `index.html` y en la línea ~5 del script, reemplazá:

```js
const SHEET_ID = 'TU_SHEET_ID_AQUI';
const SHEET_NAME = 'Detalle mensual real'; // nombre exacto de la pestaña
```

Por:

```js
const SHEET_ID = '1ThZvjoiw2J8-mSoPnvfYJyh9kHl2S3Rs';
const SHEET_NAME = 'Nombre exacto de la pestaña';
```

---

### 4. Crear el repo y publicar en GitHub Pages

```bash
# Desde la carpeta del proyecto
git init
git add .
git commit -m "feat: veta dashboard financiero v1"

# Crear repo en GitHub (sin README, sin .gitignore)
git remote add origin https://github.com/TU_USUARIO/veta-dashboard.git
git branch -M main
git push -u origin main
```

Luego en GitHub:
1. **Settings → Pages**
2. Source: **Deploy from a branch**
3. Branch: `main`, carpeta: `/ (root)`
4. Guardar

En ~1 minuto el dashboard estará en:
`https://TU_USUARIO.github.io/veta-dashboard/`

---

## Estructura del proyecto

```
veta-dashboard/
├── index.html     # Dashboard completo (single-file)
└── README.md      # Este archivo
```

---

## Secciones del dashboard

| Sección | Contenido |
|---|---|
| **Resumen** | KPIs, ingresos vs costos, margen, mix de clientes |
| **Comparativa interanual** | Tabla y gráficos superpuestos 2024/25/26 |
| **Clientes** | Activos vs churned, ingresos por cliente, heatmap de actividad |
| **Costos y sueldos** | Estructura por rol, evolutivo mensual, comparativa interanual |
| **Dividendos** | Por socio, resultado vs distribuido, interanual |

---

## Actualización de datos

### Opción A — Datos desde Sheets (recomendado)
Con el sheet publicado y el SHEET_ID configurado, el dashboard se actualiza automáticamente en cada visita — sin tocar código.

### Opción B — Actualización manual del fallback
Si no usás Sheets live, los datos hardcodeados están en el objeto `FALLBACK` dentro de `index.html` (~línea 100). Actualizalo mensualmente.

---

## Notas de privacidad

- El sheet publicado es **solo lectura** y solo expone los datos crudos de la hoja seleccionada
- No hay autenticación en el dashboard — cualquiera con la URL puede verlo
- Si necesitás acceso restringido, mové el repo a privado y usá GitHub Pages con restricción de acceso (requiere plan GitHub Teams)
