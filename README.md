# 🗺 Reporte de Tianguis – Querétaro

Aplicación web para visualizar corredores comerciales informales (tianguis) en un mapa interactivo.

## ✨ Funcionalidades

- Polígonos en el mapa por cada tianguis (colores distintos)
- Click en un corredor → panel lateral con:
  - Datos generales (nombre, descripción, horario, locales, antigüedad)
  - Área calculada automáticamente del polígono (m²)
  - Distancia en metros al otro corredor (entre centroides)
  - Lista de problemas con severidad (alta / media / baja)
  - Información de contacto
- Mapa oscuro estilo urbano (CartoDB Dark)
- Sin API keys requeridas

---

## 📁 Estructura

```
tianguis-reporte/
├── index.html          ← App principal
├── vercel.json         ← Config para Vercel
├── README.md
└── data/
    └── tianguis.json   ← ⚙️ EDITA AQUÍ los datos de los tianguis
```

---

## ✏️ Cómo editar los datos

Abre `data/tianguis.json`. Cada tianguis tiene esta estructura:

```json
{
  "id": "tianguis-nombre",
  "nombre": "Nombre del Corredor",
  "descripcion": "Descripción breve...",
  "color": "#e63946",           ← color del polígono (hex)
  "colorNombre": "Rojo",
  "diasOperacion": "Domingos",
  "horario": "6:00 AM – 3:00 PM",
  "numeroLocales": 148,
  "antiguedad": "Más de 20 años",
  "responsable": "Nombre de la organización",
  "telefono": "442-123-4567",
  "categoria": "Mixto",
  "problemas": [
    {
      "id": 1,
      "titulo": "Nombre del problema",
      "descripcion": "Descripción del problema...",
      "severidad": "alta"        ← alta | media | baja
    }
  ],
  "coordenadas": [
    [LAT, LNG],                  ← pares [latitud, longitud]
    [LAT, LNG],
    ...
    [LAT, LNG]                   ← repetir primera coord para cerrar el polígono
  ]
}
```

### 🗺 Cómo obtener coordenadas del polígono

1. Ve a [geojson.io](https://geojson.io)
2. Dibuja el polígono sobre el mapa
3. Copia las coordenadas del JSON generado
4. Invierte el orden: GeoJSON usa `[lng, lat]`, aquí se usa `[lat, lng]`

---

## 🚀 Deploy en Vercel

### Opción A – GitHub + Vercel (recomendado)

```bash
# 1. Crear repo en GitHub
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/TU_USUARIO/tianguis-reporte.git
git push -u origin main

# 2. Ve a vercel.com → New Project → importa el repo → Deploy
```

### Opción B – Vercel CLI

```bash
npm i -g vercel
vercel
```

---

## 🔧 Desarrollo local

```bash
# Con Python (sin instalación)
python3 -m http.server 8080

# Abrir: http://localhost:8080
```

> ⚠️ No abras `index.html` directo con doble click – el fetch del JSON requiere un servidor local.

---

## 🛠 Stack técnico

| Herramienta | Uso |
|---|---|
| [Leaflet.js](https://leafletjs.com) | Mapa interactivo (gratuito, sin API key) |
| [CartoDB Dark](https://carto.com/basemaps) | Tiles del mapa oscuro (gratuito) |
| [Turf.js](https://turfjs.org) | Cálculo de área y distancia geoespacial |
| HTML + CSS + JS vanilla | Sin frameworks, carga instantánea |
| Vercel | Hosting gratuito |