# Análisis de Publicaciones en Hacker News

Este proyecto analiza un conjunto de datos de publicaciones de Hacker News para determinar qué tipo de publicaciones reciben más comentarios y si la hora de creación de una publicación afecta la cantidad de comentarios que recibe.

## Introducción

Hacker News es un sitio de noticias sociales centrado en la informática y el espíritu empresarial. En este proyecto, comparamos dos tipos de publicaciones:

- **Ask HN**: Publicaciones en las que los usuarios hacen una pregunta específica a la comunidad de Hacker News.
- **Show HN**: Publicaciones en las que los usuarios muestran un proyecto, producto o algo interesante a la comunidad de Hacker News.

## Diccionario de Datos

El conjunto de datos utilizado en este análisis contiene la siguiente información para cada publicación:

- `id`: El identificador único de la publicación en Hacker News.
- `title`: El título de la publicación.
- `url`: La URL a la que enlaza la publicación.
- `num_points`: El número de puntos que ha adquirido la publicación.
- `num_comments`: El número de comentarios de la publicación.
- `author`: El nombre de usuario de la persona que envió la publicación.
- `created_at`: La fecha y hora de envío de la publicación.

## Análisis

El análisis realizado en este proyecto incluye los siguientes pasos:

1.  **Carga y limpieza de datos**: Se carga el conjunto de datos y se eliminan las cabeceras.
2.  **Extracción de publicaciones "Ask HN" y "Show HN"**: Se filtran las publicaciones para separar las que son "Ask HN" y "Show HN" del resto.
3.  **Cálculo del número promedio de comentarios**: Se calcula el número promedio de comentarios para las publicaciones "Ask HN" y "Show HN".
4.  **Análisis por hora de creación**: Se analiza si la hora del día en que se crea una publicación "Ask HN" afecta la cantidad de comentarios que recibe.

## Hallazgos

-   Las publicaciones de **"Ask HN"** reciben un promedio de **10.39 comentarios**, mientras que las publicaciones de **"Show HN"** reciben un promedio de **4.89 comentarios**.
-   Las publicaciones de "Ask HN" creadas durante las **15:00** (3 PM) reciben la mayor cantidad de comentarios en promedio.

## Conclusión

Según el análisis, para obtener una mayor cantidad de comentarios en una publicación de Hacker News, se recomienda:

-   Crear una publicación de tipo **"Ask HN"**.
-   Publicarla alrededor de las **15:00** (3 PM).
