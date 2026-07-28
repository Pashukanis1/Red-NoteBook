# TUI Calendar

> Un calendario de escritorio 100% local para Windows, con la estética de una interfaz de terminal (TUI) y la potencia de organización de Google Calendar.

![Platform](https://img.shields.io/badge/platform-Windows-blue) ![Made with Electron](https://img.shields.io/badge/made%20with-Electron-47848F) ![Local first](https://img.shields.io/badge/datos-100%25%20locales-brightgreen) ![License](https://img.shields.io/badge/license-MIT-lightgrey)

<img width="1912" height="1023" alt="图片" src="https://github.com/user-attachments/assets/35d4b543-9600-4089-88c3-76b98de925a2" />
<img width="1917" height="991" alt="图片" src="https://github.com/user-attachments/assets/f2ca34a2-653a-47a1-9e74-dfff60c71484" />
<img width="1917" height="1015" alt="图片" src="https://github.com/user-attachments/assets/6cb123ee-66c1-499a-990c-abb695486926" />
<img width="1917" height="1032" alt="图片" src="https://github.com/user-attachments/assets/a350266e-d894-48a0-86b3-3e4995b3a531" />

TUI Calendar no depende de ningún servidor ni de internet para funcionar. Todos tus eventos, calendarios y preferencias se guardan en tu propia máquina — nada se sube a la nube.

---

## Tabla de contenidos

- [Características](#características)
- [Capturas](#capturas)
- [Instalación](#instalación)
- [Uso en modo desarrollo](#uso-en-modo-desarrollo)
- [Generar el instalador (.exe)](#generar-el-instalador-exe)
- [Dónde se guardan tus datos](#dónde-se-guardan-tus-datos)
- [Estructura del proyecto](#estructura-del-proyecto)
- [Roadmap](#roadmap)
- [Licencia](#licencia)

---

## Características

### 🖥️ Estética Terminal User Interface
Bordes rectos, tipografía monoespaciada, resaltados de selección estilo `>`, checkboxes en formato `[x]` / `[ ]`, y paneles con la sobriedad visual de una consola — sin sacrificar nada de la usabilidad de un calendario moderno.

### 📅 Función compleja de eventos
Creación de eventos con título, fecha, hora y color, más:
- **Eventos de día completo** (`[Nombre del evento]` bajo la fecha, sin bloque de 24 horas).
- **Recurrencia avanzada**: diaria, semanal, mensual o anual, con fin "nunca", por fecha límite o por cantidad de repeticiones — incluyendo patrones especiales como "mismo día y mes cada año" o "día exacto del mes durante X meses, a lo largo de Y años".
- **Edición por instancia o por serie completa**, con excepciones individuales dentro de una serie recurrente.
- Eventos superpuestos se acomodan automáticamente en columnas, sin taparse entre sí.
- Arrastrar y redimensionar eventos directamente sobre la cuadrícula.

### 🗂️ Múltiples calendarios
Organiza tus eventos en distintos calendarios/categorías (Trabajo, Personal, etc.), cada uno con su propio color y su propio interruptor de visibilidad — ocultá el que no quieras ver sin borrar nada.

### 📌 Modo Widget
Un panel flotante y minimalista, independiente de la ventana principal, que muestra tu agenda del día y el estado del Pomodoro en todo momento — ideal para mantener un ojo en tu día sin ocupar toda la pantalla.

### 🎨 Personalización absoluta
Casi cualquier color de la interfaz es editable: líneas de días y horas, resaltados, fondo de eventos, colores del Pomodoro, y más — a través de una paleta propia con secciones predefinidas (**Vibrantes**, **Pastel**, **Oasis**, **Otoño**) y una sección **Personalizada** de 12 espacios, cada uno editable con un selector Hex construido enteramente con caracteres de dibujo de caja (`║ ═ ╔ ╗ ╚ ╝`) para mantener la estética TUI incluso en sus controles más pequeños. También podés elegir la fuente por sección de la interfaz y el grosor de la barra de scroll.

### 🍅 Pomodoro integrado
Temporizador Pomodoro completamente configurable (minutos de trabajo, minutos de descanso, cantidad de sesiones), con una barra de progreso visible y alarma sonora al cambiar de etapa — accesible como una pestaña desplegable desde la barra de herramientas.

### 🔭 Múltiples vistas
Igual que Google Calendar: **Día**, **3 Días**, **Semana**, **Mes** y **Año**, todas con navegación (Hoy / ‹ / ›) y la misma estética TUI.

### 🌫️ Fondo transparente
Efecto vidrio esmerilado (Acrylic nativo de Windows): tu escritorio se ve difuminado detrás de la ventana, sin depender de librerías externas.

### 🖼️ Fondo de imagen personalizada
Elegí cualquier imagen de tus archivos como fondo de la aplicación, con la opción de alternar entre el modo vidrio y el modo imagen cuando quieras.

---

## Capturas

*(Agregá aquí capturas de pantalla de tu instalación — por ejemplo `docs/screenshot-week.png`, `docs/screenshot-month.png`, `docs/screenshot-settings.png`.)*

```md
![Vista semanal](docs/screenshot-week.png)
![Personalización](docs/screenshot-settings.png)
```

---

## Instalación

### Requisitos

- Windows 10/11
- [Node.js](https://nodejs.org/) (solo necesario para compilar; la app ya compilada no lo requiere)

### Instalar el ejecutable

Descargá el instalador `.exe` generado (ver [Generar el instalador](#generar-el-instalador-exe)) y ejecutalo. La app queda disponible como cualquier programa de Windows, sin dependencias adicionales.

---

## Uso en modo desarrollo

```bash
git clone <url-de-tu-repositorio>
cd tui-calendar
npm install
npm start
```

`npm install` necesita internet solo para descargar Electron la primera vez — la aplicación en sí funciona completamente offline.

---

## Generar el instalador (.exe)

```bash
npm install
npm run dist
```

Esto genera un instalador NSIS standalone dentro de la carpeta `dist/`, listo para compartir o distribuir en cualquier PC con Windows.

> El ícono de la app se toma de `assets/icon.ico`. Si querés cambiarlo, reemplazá ese archivo por uno propio (formato `.ico`, con un frame cuadrado de al menos 256×256).

---

## Dónde se guardan tus datos

Todo se guarda localmente en:

```
%APPDATA%\tui-calendar\
├─ events.json     -> tus eventos y calendarios
├─ settings.json   -> tu personalización (colores, fuentes, fondo, etc.)
└─ backgrounds\     -> imagen de fondo elegida, si aplica
```

No hay sincronización con la nube ni telemetría de ningún tipo.

---

## Estructura del proyecto

```
tui-calendar/
├─ main.js            -> proceso principal de Electron (ventanas, IPC, archivos, fondo)
├─ preload.js         -> puente seguro entre main y las interfaces
├─ src/
│  ├─ index.html      -> estructura de la ventana principal
│  ├─ style.css       -> estética TUI y estilos de cada vista
│  ├─ renderer.js     -> lógica de vistas, eventos, calendarios, personalización y Pomodoro
│  ├─ widget.html     -> estructura del modo Widget
│  └─ widget.js       -> lógica del panel Widget
├─ assets/            -> ícono de la app
└─ package.json
```

---

## Roadmap

Ideas para próximas versiones:

- [ ] Notas y ubicación en el evento
- [ ] Eventos que abarcan varios días
- [ ] Importar/exportar en formato `.ics`
- [ ] Recordatorios y notificaciones de escritorio
- [ ] Bandeja del sistema e inicio automático con Windows
- [ ] Copias de seguridad automáticas de tus datos

---

## Licencia

[MIT](LICENSE)
