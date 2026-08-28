# CONTEXT.md

Documento de retomada. Estado real a fecha 2026-08-28 (último commit: 2026-02-05).

## 1. Qué es

Colección de proyectos de análisis de datos realizados durante la ruta de
aprendizaje del autor en Dataquest.io. Cada carpeta numerada es un proyecto
independiente y autocontenido (dataset + notebook Jupyter + README) que
demuestra habilidades prácticas de Python, pandas, limpieza de datos y
visualización. No es una aplicación: es un portfolio de notebooks.

## 2. Stack

- **Lenguaje:** Python 3.8 (según `package_libraries.txt`).
- **Librerías núcleo:** pandas 1.0.5, numpy 1.18.5, matplotlib 3.2.2. También
  presentes en el entorno original: seaborn, scikit-learn, statsmodels, plotly,
  chardet (detección de encoding), nltk. No todas se usan en todos los proyectos.
- **Entorno de ejecución:** Jupyter Lab / Notebook.
- **Gestión de dependencias:** inconsistente (ver Decisiones). Solo el proyecto 00
  tiene un `package_libraries.txt` (export de `conda list`, no un requirements
  instalable directamente). Los README mencionan un `requirements.txt` con
  `pandas`/`numpy` que **no existe en el repo**.
- **Despliegue:** ninguno. Repo alojado en GitHub (`origin/main`,
  github.com/albertjimrod). Sin CI, sin empaquetado, sin hosting.

## 3. Arquitectura

Estructura plana: un directorio por proyecto en la raíz, más un `README.md`
índice general. Cada proyecto contiene:

- Uno o varios notebooks `.ipynb` (el análisis destilado suele estar en un
  notebook "consolidado"/"merged"/"best"; conviven con notebooks de notas/estudio).
- Los datasets en CSV (a veces bajo subcarpeta `csv/`), y alguna imagen de
  cabecera (`.jpg`/`.jpeg`/`.png`).
- Un `README.md` propio (salvo los proyectos 05 y 06, que no lo tienen).

Inventario de proyectos:

| # | Carpeta | Notebook principal | Dataset(s) | Tema |
|---|---------|--------------------|------------|------|
| 00 | Profitable App Profiles... | `Profitable App Profiles For The App Store And Google Play Markets.ipynb` | `csv/AppleStore.csv`, `csv/googleplaystore.csv` | Perfiles de apps rentables (modelo freemium, apps en inglés, géneros más populares) |
| 01 | Exploring Hacker News Posts | `Hacker_News_Merged_Analysis_v2.ipynb` | `HN_posts_year_to_Sep_26_2016.csv` | Ask HN vs Show HN; comentarios por hora de publicación |
| 02 | Exploring eBay Car Sales Data | `Exploring Ebay Car Sales Data v2.ipynb` | `csv/autos.csv` | Limpieza de coches usados de eBay Kleinanzeigen; análisis de outliers de precio |
| 04 | Finding Heavy Traffic Indicators on I-94 | `Traffic on the I-94 Interstate highway.ipynb` | (dataset I-94, PENDIENTE DE CONFIRMAR su presencia en la carpeta) | Indicadores de tráfico denso: hora, día, mes, clima |
| 05 | Storytelling Data Visualization on Exchange Rates | `Best_Analysis_Exchange_Rates.ipynb` (+ notebook de notas) | (serie de tipos de cambio euro-referenciada; PENDIENTE DE CONFIRMAR archivo) | Data storytelling con matplotlib sobre tipos de cambio |
| 06 | Clean and Analyze Employee Exit Surveys | `Guided Project Clean and Analyze Employee Exit Surveys sweet-anotaciones_estudio_a.ipynb` | `dete_survey.csv`, `tafe_survey.csv` | Combinar y limpiar encuestas de salida de empleados (DETE + TAFE) |

No hay proyecto "03" (hueco en la numeración; PENDIENTE DE CONFIRMAR si fue
eliminado o nunca existió). El README del proyecto 04 está desactualizado:
describe rutas de notebooks externas y un segundo proyecto de "Car Price
Prediction" que no está en este repo.

## 4. Decisiones clave

- **Un notebook consolidado por proyecto.** Se fusionaron los notebooks de pasos
  del curso en un único notebook de análisis limpio (nombres "Merged", "v2",
  "Best", "Consolidated"). Los notebooks de notas/estudio se conservan en paralelo
  en algunos proyectos (05, 06).
- **Idioma mixto.** Los README de 01 y algunos notebooks/anotaciones están en
  español; los de 00, 02, 04 en inglés. En el proyecto 02 se tradujeron además
  las categorías originales en alemán a español/inglés.
- **Detección de encoding con `chardet`** antes de cargar CSVs (proyectos 00, 02)
  en lugar de asumir UTF-8, para evitar errores de lectura.
- **Nomenclatura `snake_case`** para columnas: en el proyecto 02 se renombraron
  las columnas de `camelCase` del origen a `snake_case`.
- **Limpieza selectiva de outliers** (proyecto 02): en vez de descartar en bloque
  los precios altos, se investigaron uno a uno; se conservaron vehículos de lujo
  legítimos (Ferrari, Rolls Royce) y se corrigió manualmente un precio erróneo de
  un Maserati clásico según investigación de mercado. Alternativa descartada:
  recorte ciego por percentil.
- **Se dejaron de rastrear ficheros no necesarios** para el análisis (commits
  `cab9a62`, `b364c70` — este último eliminó del historial una clave pública SSH
  commiteada por error). El proyecto 02 tuvo un borrado y re-adición completa de
  contenido (`7d1acd8` → `05ddd5f`).
- **Sin gestión de dependencias formal.** Decisión implícita: al ser notebooks de
  curso no se añadió `requirements.txt`/`pyproject.toml` real. Los README lo
  mencionan pero el fichero no se creó. PENDIENTE DE CONFIRMAR si se quiere
  normalizar.

## 5. Estado actual

- **Funciona:** los 6 proyectos están completos con su análisis y conclusiones.
  El README raíz (commit más reciente, `b99c37a`) sirve de índice y está al día
  respecto a las carpetas existentes.
- **Rama activa:** solo `main`, actualizada con `origin/main`. Sin otras ramas.
- **Cambios sin commitear:** 5 ficheros aparecen como modificados en
  `git status`, pero `git diff --stat` reporta **0 inserciones / 0 borrados** en
  todos ellos (2 notebooks de "notas" del proyecto 05, `exchange_rates.jpeg`
  idéntico byte a byte 131836→131836, y `dete_survey.csv` / `tafe_survey.csv` del
  proyecto 06). Son cambios de metadatos (modo de fichero, fin de línea o mtime),
  **sin cambios de contenido**. Se pueden descartar con `git checkout -- .` sin
  pérdida. PENDIENTE DE CONFIRMAR la causa exacta (probable `core.autocrlf` o
  `filemode`).
- **Deuda / inconsistencias conocidas:**
  - README del proyecto 04 desactualizado (rutas externas, proyecto de ML ajeno).
  - Proyectos 05 y 06 sin README propio.
  - Nombres de notebook en los README no siempre coinciden con el fichero real
    (p. ej. 02 menciona `Ebay_Car_Sales_Analysis_Consolidated.ipynb`; el fichero
    es `Exploring Ebay Car Sales Data v2.ipynb`).
  - `.ipynb_checkpoints/` versionado en el proyecto 05 (debería ignorarse).
  - Hueco en la numeración (no hay `03_`).
  - `requirements.txt` referenciado pero inexistente.

## 6. Próximos pasos (priorizados)

1. Limpiar el working tree: `git checkout -- .` para descartar los 5 "cambios"
   vacíos y dejar `git status` limpio.
2. Añadir un `.gitignore` en la raíz con `.ipynb_checkpoints/` y quitar del
   índice los checkpoints ya versionados (proyecto 05).
3. Escribir README para los proyectos 05 y 06, siguiendo el formato de 00–02.
4. Corregir el README del proyecto 04 (describe contenido que no está en el repo).
5. Alinear en cada README el nombre del notebook principal con el fichero real.
6. Decidir política de dependencias: o crear un `requirements.txt` mínimo real
   (pandas, numpy, matplotlib, seaborn, chardet, jupyter) en la raíz, o quitar
   las referencias a `requirements.txt` de los README.
7. Aclarar el hueco del proyecto 03 (documentarlo o renumerar).
8. Opcional: unificar idioma de los README (todo español o todo inglés).
