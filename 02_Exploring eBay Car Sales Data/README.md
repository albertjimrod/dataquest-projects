
# Análisis de Datos de Ventas de Coches en eBay

Este proyecto realiza una limpieza y análisis exploratorio de un conjunto de datos de coches de segunda mano extraído de eBay Kleinanzeigen, la sección de anuncios clasificados de la web alemana de eBay.

El notebook consolidado, `Ebay_Car_Sales_Analysis_Complete.ipynb`, es el resultado de unificar las mejores prácticas y fragmentos de código de varias versiones de análisis previas.

## Conjunto de Datos

El dataset original, `autos.csv`, fue obtenido de Kaggle y contiene 50,000 registros de anuncios de coches.

- **Fuente Original:** [Used Cars Dataset en Data.world](https://data.world/data-society/used-cars-data)

## Análisis Realizado

El notebook sigue un flujo de trabajo estructurado para limpiar, analizar y visualizar los datos. Los pasos clave incluyen:

1.  **Carga y Limpieza Inicial:**
    -   Carga del dataset con la codificación de caracteres correcta (`Windows-1252`).
    -   Renombrado de columnas de `camelCase` a `snake_case` para seguir las convenciones de Python.
    -   Eliminación de columnas irrelevantes que no aportan valor al análisis (ej. `seller`, `offerType`, `nr_pictures`).

2.  **Limpieza de Columnas Numéricas:**
    -   Conversión de las columnas `price` y `odometer` de texto a tipo numérico, eliminando caracteres no deseados como `$` y `km`.

3.  **Traducción de Datos Categóricos:**
    -   Mapeo de los términos en alemán de columnas como `vehicle_type` y `fuel_type` a sus equivalentes en español para facilitar la comprensión del análisis.

4.  **Manejo de Valores Atípicos (Outliers):**
    -   Análisis detallado de los valores atípicos en las columnas de precio y año de matriculación.
    -   En lugar de una eliminación ciega, se investigan los valores extremos para determinar si son realistas (ej. coches de lujo con precios elevados).
    -   Se establece un rango de precios y años razonable para filtrar el dataset y obtener resultados más fiables.

5.  **Análisis Exploratorio y Agregación:**
    -   Cálculo del precio medio y el kilometraje medio para las marcas de coches más populares.
    -   Creación de un DataFrame agregado que resume esta información para una fácil comparación entre marcas.

## Requisitos

Para ejecutar este notebook, necesitas tener instaladas las siguientes librerías. Puedes instalarlas usando `pip`:

```
pip install -r requirements.txt
```

Contenido del archivo `requirements.txt`:

```
pandas
numpy
matplotlib
seaborn
chardet
```

## Cómo Ejecutar

1.  Asegúrate de tener el archivo `autos.csv` en el mismo directorio que el notebook.
2.  Instala las dependencias listadas en el archivo `requirements.txt`.
3.  Inicia Jupyter Lab o Jupyter Notebook:
    ```bash
    jupyter lab
    ```
4.  Abre el archivo `Ebay_Car_Sales_Analysis_Complete.ipynb` y ejecuta las celdas.
