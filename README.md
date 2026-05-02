# ¿Dónde están mis cosas? 🔑

Aplicación web progresiva (PWA) ligera para registrar dónde dejas tus **llaves** y tu **cartera**. Incluye opcionalmente captura de **ubicación GPS** al registrar.

Hecha con HTML + CSS + JavaScript puro. Sin frameworks, sin dependencias, sin build step. Solo abrirla en el navegador y funciona.

## ✨ Características

- 📌 Dos objetos rastreables: **llaves** y **cartera** (cada uno con su propio historial)
- 🏠 3 ubicaciones predefinidas por objeto (entrada, coche, bolsillo)
- ✏️ Opción **"Otro lugar"** para escribir cualquier sitio personalizado
- 🛰️ **Captura GPS opcional** con enlace a Google Maps
- 📜 Historial de las últimas 5 ubicaciones por objeto con fecha y hora
- 💾 Persistencia en `localStorage` (los datos se quedan en el móvil)
- 📱 **Instalable como app** en Android/iOS (PWA con icono propio en la pantalla de inicio)
- 🌐 **Funciona offline** gracias al service worker
- 🎨 Sin dependencias externas — todo en HTML/CSS/JS plano

## 📁 Estructura del proyecto

```
llaves-pwa/
├── index.html      ← Toda la app (HTML, CSS y JS en un único archivo)
├── manifest.json   ← Configuración PWA (nombre, iconos, colores)
├── sw.js           ← Service worker para funcionamiento offline
├── icon-192.png    ← Icono 192x192 para Android
└── icon-512.png    ← Icono 512x512 para Android (alta resolución)
```

## 🚀 Cómo usarla

### Opción A — Desplegada en GitHub Pages

Abre la URL del proyecto en Chrome del móvil → menú ⋮ → **"Añadir a pantalla de inicio"** o **"Instalar app"**.

### Opción B — Probarla localmente

```bash
git clone https://github.com/TU-USUARIO/llaves-pwa.git
cd llaves-pwa
# Servirla con cualquier servidor HTTP local
python3 -m http.server 8000
# Abrir http://localhost:8000 en el navegador
```

> ⚠️ **Importante**: para que el GPS y la instalación como PWA funcionen, la app debe servirse por **HTTPS** (o `localhost` para pruebas). En GitHub Pages el HTTPS viene activado por defecto.

## 🛠️ Cómo modificarla

Toda la lógica está en un único `index.html`. Las zonas más interesantes para personalizar:

### Cambiar las ubicaciones predefinidas

Busca la constante `ITEMS` en el `<script>` de `index.html`:

```js
const ITEMS = {
  llaves: {
    name: "llaves",
    article: "las",
    locations: [
      { id: "entrada", label: "En el cesto de la entrada", short: "Cesto de la entrada" },
      { id: "coche",   label: "En la guantera del coche",  short: "Guantera del coche" },
      { id: "bolsillo", label: "En mi bolsillo",            short: "En tu bolsillo" },
    ],
  },
  // ...
};
```

### Añadir un nuevo objeto rastreable (ej. "gafas")

1. Añadir una entrada en `ITEMS` con sus 3 ubicaciones
2. Añadir un nuevo `<button class="tab" data-item="gafas">` en el HTML, junto a los de llaves/cartera
3. Asegurarse de que `state` tenga la clave `gafas` (la función `load()` lo crea automáticamente)

### Cambiar colores

Las clases CSS usan estos colores:

| Ubicación | Color | Hex |
|-----------|-------|-----|
| Entrada   | Ámbar | `#f59e0b` |
| Coche     | Azul  | `#3b82f6` |
| Bolsillo  | Verde | `#10b981` |
| Otro      | Morado | `#a855f7` |

## 🌐 Desplegar en GitHub Pages

1. Sube el repo a GitHub (público o privado con Pro)
2. Ve a **Settings → Pages**
3. En *Source* selecciona la rama `main` y carpeta `/ (root)`
4. Pulsa **Save**
5. En 1-2 minutos la app está disponible en `https://TU-USUARIO.github.io/llaves-pwa/`

## 🤝 Contribuir

Si quieres añadir o cambiar algo:

1. Haz un fork del repo
2. Crea una rama: `git checkout -b mejora-historial`
3. Haz tus cambios y commits
4. Abre un Pull Request describiendo qué cambia y por qué

## 📝 Licencia

MIT — haz lo que quieras con el código, siempre que mantengas la atribución.

## 🛣️ Ideas para futuras mejoras

- [ ] Botón para borrar el historial
- [ ] Más objetos personalizables por el usuario (sin tener que tocar código)
- [ ] Mini-mapa embebido en lugar del enlace a Google Maps
- [ ] Calcular distancia desde la posición actual al lugar guardado
- [ ] Notificación push si llevas mucho tiempo sin actualizar la ubicación
- [ ] Exportar/importar el historial como JSON
- [ ] Modo oscuro
