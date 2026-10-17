# Data Jam 2026 · Seguridad a base de localidades/años en Bogotá

Tablero de análisis de **delitos por localidad y año** en Bogotá, junto con la ubicación de los **CAI** (Comandos de Atención Inmediata) y las **estaciones de policía**. El proyecto tiene dos entregables que muestran la misma información:

1. **Tablero en Power BI** (`.pbix`).
2. **Página web** (`.html`) que replica el diseño y la estructura del tablero, con los datos incrustados.

> Proyecto desarrollado para el **Data Jam 2026** de la Alcaldía de Bogotá.

---

## Vista previa

| Página 1 · Delitos por localidad y año | Página 2 · CAI y estaciones |
|---|---|
| ![Página 1](assets/pagina-1.png) | ![Página 2](assets/pagina-2.png) |

**Demo web:** [ENLACE A LA DEMO]

---

## Contenido del repositorio

```
.
├── README.md
├── powerbi/
│   └── data_jam_2026.pbix          # Tablero de Power BI
├── web/
│   └── data_jam_2026.html          # Página web (un solo archivo, funciona sin conexión a datos)
├── data/
│   ├── delitos_por_localidad_anio_total.csv
│   ├── Cai.csv
│   └── Estacion.csv
└── assets/
    ├── fondo.png                   # Fondo de Bogotá desenfocado
    ├── logo-bogota.png             # Logo
    ├── pagina-1.png                # Capturas del tablero
    └── pagina-2.png
```

> Ajusta los nombres y rutas si tu carpeta es distinta.

---

## Datos

Los datos están en tres tablas CSV dentro de `data/`.

### `delitos_por_localidad_anio_total.csv`
Total de delitos por localidad y año (2018 a 2025). El tablero y la página usan **2024 y 2025**.

| Columna | Descripción |
|---|---|
| `codigo_localidad` | Código de la localidad (`01` a `20`; `99` = Sin Localización) |
| `localidad` | Nombre de la localidad |
| `anio` | Año del registro |
| `total_delitos` | Total de delitos registrados |

### `Cai.csv`
158 Comandos de Atención Inmediata. Campos que usa el proyecto:

| Columna | Descripción |
|---|---|
| `CAINOMBRE` | Nombre del CAI |
| `CAIDIR_SIT` | Dirección |
| `CAIIULOCAL` | Código de la localidad (se une con `codigo_localidad`) |
| `CAILATITUD` / `CAILONGITU` | Coordenadas |

### `Estacion.csv`
21 estaciones de policía. Campos que usa el proyecto:

| Columna | Descripción |
|---|---|
| `EPONOMBRE` | Nombre de la estación |
| `EPODIR_SIT` | Dirección |
| `EPOIULOCAL` | Código de la localidad (se une con `codigo_localidad`) |
| `EPOLATITUD` / `EPOLONGITU` | Coordenadas |

**Fuente de los datos:** [COMPLETAR: portal o entidad de donde salen los CSV].

### Notas sobre los datos

- **Sin Localización:** en 2025 hay 54.984 delitos sin localidad asignada (cerca del 21 % del total de 261.803), frente a 1.730 en 2024. Conviene tenerlo presente al comparar localidades entre años.
- **Localidades sin CAI:** Sumapaz y los registros sin localización no tienen CAI asociados, por eso no aparecen en la tabla de Totales.

---

## Tablero en Power BI

### Modelo
- Tabla de hechos: delitos por localidad y año.
- Tablas de CAI y estaciones, relacionadas con las localidades por el código (`CAIIULOCAL` y `EPOIULOCAL` hacia `codigo_localidad`).

### Página 1: delitos por localidad y año
- **Localidades:** segmentación para elegir una localidad.
- **Años entre 2024/2025:** segmentación por año.
- **Suma de total_delitos por 2024/2025:** columnas con el total de cada año.
- **Tarjetas 2024 y 2025:** total de delitos de cada año.
- **Suma de total_delitos por localidad:** barras horizontales ordenadas de mayor a menor.
- **Totales:** tabla con localidad, total de delitos, nombre del CAI y dirección.

### Página 2: CAI y estaciones
- **Estaciones de policía Bogotá:** mapa con la ubicación de las estaciones.
- **Cai Bogotá:** mapa con la ubicación de los CAI.

### Advertencia: separador decimal
Los CSV guardan los totales como `20569.0`. Si Power BI está en configuración regional de Colombia, puede leer el punto como separador de miles y convertir `20569.0` en `205690`, lo que **multiplica todas las cifras por 10**. Para evitarlo, en Power Query:

1. Selecciona la columna `total_delitos`.
2. **Cambiar tipo > Usando configuración regional...**
3. Tipo de datos: *Número decimal* o *Número entero*, configuración regional: *Inglés (Estados Unidos)*.

Después de corregirlo, los totales de la ciudad deben ser **238.100 delitos en 2024** y **261.803 en 2025**.

---

## Página web

Réplica del tablero en un solo archivo HTML, sin frameworks ni dependencias de datos externas: los datos van incrustados.

### Qué incluye
- El mismo diseño y la misma estructura de las dos páginas del tablero, con fondo de Bogotá y lienzo azul suave.
- Filtros por localidad y por año que actualizan el resto de gráficos, las tarjetas, la tabla y los mapas. También se puede filtrar haciendo clic en las barras.
- Tabla de Totales con encabezado y fila de total fijos.
- Mapas de CAI y estaciones con zoom y arrastre, y nombre de la localidad en cada punto.
- Diseño adaptable a celular y modo claro/oscuro.

### Tecnologías
HTML, CSS y JavaScript puro. Tipografía Barlow Semi Condensed desde Google Fonts (con tipografías de respaldo).

### Cómo usarla
Abre `web/data_jam_2026.html` con doble clic en cualquier navegador, o publícala con GitHub Pages:

1. En el repositorio ve a **Settings > Pages**.
2. En *Source* elige la rama y la carpeta donde está el HTML (puedes renombrarlo a `index.html`).
3. Guarda y abre el enlace que genera GitHub.

### Limitaciones
- Los mapas dibujan puntos por coordenadas, **sin calles ni mapa base**, porque la página no carga teselas externas.
- Si los CSV cambian, hay que volver a incrustar los datos en el HTML.

---

## Equipo

| Nombre | Rol |
|---|---|
| [NOMBRE] | [ROL] |
| [NOMBRE] | [ROL] |

## Licencia

[COMPLETAR: por ejemplo MIT para el código; verifica las condiciones de uso de los datos y del logo de Bogotá.]
