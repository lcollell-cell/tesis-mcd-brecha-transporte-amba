# Brecha entre tiempo programado y observado en el transporte público del AMBA

Tesis de Maestría en Ciencia de Datos (ITBA). Autor: Leandro Collell. Director: Ariel Salgado Corrado.

Accesibilidad a servicios básicos (hospital, escuela, supermercado, centro) hasta el tercer cordón del AMBA,
comparando el tiempo **programado** (GTFS + OpenStreetMap con r5py) con el tiempo **estimado por Google Maps**
(Routes API, modo tránsito). La Línea 51 es el caso de validación (hipótesis H1 y H2 del TFI).

## Estructura

| Carpeta | Contenido |
|---|---|
| `data/raw` | Datos originales, sin modificar (no se versionan; ver `docs/DATOS.md`) |
| `data/interim`, `data/processed` | Resultados intermedios y tablas finales |
| `notebooks/` | Un notebook por fase: `01_programado`, `02_piloto_api`, `03_toma_google`, `04_modelos`, `05_validacion_l51` |
| `src/brecha_amba/` | Funciones reutilizables (H3, ruteo, toma de datos con tope de cuota, modelos) |
| `config/` | Franjas horarias, cupo de la API y parámetros del muestreo |
| `reports/` | Figuras (formato vectorial) y tablas que regeneran los scripts |
| `docs/` | Documentación de datos: acceso, contenido y cómo se recolectó cada fuente |

## Fases

1. Base normativa (P1): GTFS + OSM con r5py, hexágonos H3.
2. Datos reales (P2): piloto de la API y toma en franjas pico y valle, dentro del cupo gratuito.
3. Modelos (P3, D1 a D3): clustering, boosting con SHAP y Moran local.
4. Cierre: validación en la Línea 51, experimentos y anexos.

## Reproducir

```bash
conda env create -f environment.yml
conda activate brecha-amba
export GOOGLE_MAPS_API_KEY=...   # solo para la fase 2; no subir la clave al repositorio
```

## Datos y licencias

- Código: MIT. Datos y documentación propios: CC BY 4.0.
- Fuentes de terceros (GTFS BA Data, KML CNRT, Viajes y etapas, Matriz O-D del BID, OpenStreetMap) conservan su licencia.
- Los tiempos de Google Maps se publican solo en la medida en que lo permitan los términos de la Routes API.

## Cómo citar

Ver `CITATION.cff`. Cada versión se archiva en Zenodo y recibe un DOI.
