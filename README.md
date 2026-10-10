
# 🎬 Taller 03 | Análisis de Redes y Sistemas de Recomendación

### Maestría en Ciencia de Datos

**Dataset:** MovieLens 100K  
**Lenguaje:** Python  
**Entorno de desarrollo:** Google Colab

---

## 📌 Descripción del proyecto

Este proyecto integra técnicas de **análisis de redes y sistemas de recomendación** para estudiar las interacciones entre usuarios y películas utilizando el conjunto de datos MovieLens 100K.

El trabajo se desarrolla en dos etapas principales:

1. **Análisis de redes:** representar las relaciones entre usuarios y películas mediante un grafo bipartito, analizar sus conexiones y explorar la detección de comunidades.
2. **Sistemas de recomendación:** implementar, evaluar y optimizar modelos de filtrado colaborativo para predecir calificaciones y recomendar películas.

El análisis se realiza en Python utilizando herramientas de ciencia de datos y aprendizaje automático.

---

## 🎯 Objetivo general

Analizar las relaciones entre usuarios y películas mediante teoría de grafos y desarrollar modelos de recomendación capaces de estimar las preferencias de los usuarios.

### Objetivos específicos

- Explorar y describir el conjunto de datos MovieLens 100K.
- Construir un grafo bipartito de usuarios y películas.
- Analizar la centralidad de grado y el coeficiente de agrupamiento.
- Aplicar Girvan-Newman para explorar la estructura de comunidades.
- Implementar modelos de recomendación SVD y KNN.
- Evaluar y optimizar los modelos mediante RMSE y GridSearchCV.
- Generar recomendaciones personalizadas de películas.

---

## 📊 1. Conjunto de datos: MovieLens 100K

MovieLens 100K contiene calificaciones de películas realizadas por diferentes usuarios.

| Característica | Resultado |
|:---|---:|
| Total de calificaciones | 100.000 |
| Usuarios únicos | 943 |
| Películas únicas | 1.682 |
| Calificación mínima | 1 |
| Calificación máxima | 5 |
| Calificación promedio | 3,53 |
| Valores faltantes | 0 |

### Distribución de calificaciones

El análisis exploratorio permitió identificar que las calificaciones de 4 y 5 estrellas son las más frecuentes.

| Calificación | Frecuencia |
|:---:|---:|
| ⭐ 1 | 6.110 |
| ⭐⭐ 2 | 11.370 |
| ⭐⭐⭐ 3 | 27.145 |
| ⭐⭐⭐⭐ 4 | 34.174 |
| ⭐⭐⭐⭐⭐ 5 | 21.201 |

**Interpretación:** aproximadamente el 55,38 % de las calificaciones corresponde a 4 o 5 estrellas, lo que muestra una mayor frecuencia de valoraciones positivas dentro del conjunto de datos.

---

## 🕸️ 2. Análisis de redes

### Construcción del grafo bipartito

Se utilizó NetworkX para construir un grafo bipartito formado por dos tipos de nodos:

- **Usuarios:** representan a las personas que calificaron películas.
- **Películas:** representan los contenidos evaluados.

Cada arista conecta un usuario con una película que ha calificado.

Esta representación permite analizar las interacciones como una red y estudiar sus propiedades estructurales.

### Centralidad de grado

Se calculó el grado de los nodos para identificar:

- Los usuarios que calificaron más películas.
- Las películas que recibieron más calificaciones.

Entre los resultados obtenidos, el usuario 405 registró 737 películas calificadas y *Star Wars (1977)* fue la película con mayor número de evaluaciones, con 583.

### Coeficiente de agrupamiento bipartito

Se utilizó una medida de agrupamiento adaptada a redes bipartitas para estudiar el solapamiento de conexiones.

En la muestra analizada se obtuvo un coeficiente promedio aproximado de **0,1013**.

Este resultado describe la muestra seleccionada y no debe interpretarse automáticamente como el valor de toda la red.

---

## 🔍 3. Detección de comunidades: Girvan-Newman

Se aplicó el algoritmo **Girvan-Newman** para explorar la división de una subred en comunidades.

Por su costo computacional, el análisis se realizó sobre una subred de:

| Característica | Cantidad |
|:---|---:|
| Nodos | 44 |
| Aristas | 295 |

### Resultados

- Primera división: comunidades de 43 y 1 nodos.
- Segunda división: comunidades de 42, 1 y 1 nodos.

**Interpretación:** el algoritmo separó progresivamente nodos de una comunidad predominante. Estas divisiones permiten explorar la estructura de la red, pero no demuestran por sí solas que los grupos tengan preferencias cinematográficas similares.

Los resultados se representaron mediante visualizaciones de redes con colores para distinguir las comunidades.

---

## 🤖 4. Sistemas de recomendación

Se implementaron dos modelos de filtrado colaborativo utilizando Scikit-Surprise.

### Modelo SVD

SVD utiliza factores latentes para aprender patrones de preferencias entre usuarios y películas.

A partir de esos patrones, estima las calificaciones que un usuario podría asignar a películas que todavía no ha evaluado.

### Modelo KNN

KNN utiliza la similitud entre usuarios para estimar calificaciones a partir de las preferencias registradas por usuarios similares.

### Preparación de datos

Para evaluar los modelos, las calificaciones se dividieron en:

- **80 %:** conjunto de entrenamiento.
- **20 %:** conjunto de prueba.

Se utilizó `random_state=42` para facilitar la reproducibilidad de la separación.

---

## 📈 5. Evaluación de modelos

Los modelos se evaluaron utilizando **RMSE (Root Mean Squared Error)**.

RMSE mide la diferencia entre las calificaciones reales y las predicciones del modelo.

**Un RMSE menor indica un menor error predictivo.**

### Resultados iniciales

| Modelo | RMSE |
|:---|---:|
| SVD | 0,9352 |
| KNN | 1,0194 |

En la evaluación inicial, SVD obtuvo un menor error que KNN.

---

## ⚙️ 6. Optimización con GridSearchCV

Se utilizó GridSearchCV para buscar combinaciones de hiperparámetros y mejorar el rendimiento de los modelos.

La búsqueda se realizó mediante validación cruzada sobre los datos de entrenamiento.

Posteriormente, las configuraciones seleccionadas se evaluaron sobre el conjunto de prueba.

### Comparación de resultados

| Modelo | RMSE inicial | RMSE optimizado |
|:---|---:|---:|
| SVD | 0,9352 | **0,9348** |
| KNN | 1,0194 | 0,9770 |

### Interpretación

- SVD obtuvo el menor RMSE en el conjunto de prueba.
- La optimización de SVD produjo una mejora pequeña.
- KNN presentó una reducción más notable de su error después de la optimización.
- Los resultados corresponden al conjunto de datos y al procedimiento de evaluación utilizados en este proyecto.

**Modelo seleccionado para las recomendaciones: SVD.**

---

## 🍿 7. Recomendaciones personalizadas

Se utilizó SVD para generar recomendaciones al **usuario 196**.

El procedimiento consistió en identificar películas que el usuario no había calificado, estimar sus puntuaciones y seleccionar las cinco con mayor valor predicho.

### Top 5 de recomendaciones

| Posición | Película | Calificación estimada |
|:---:|:---|---:|
| 1 | A Close Shave (1995) | 4,66 |
| 2 | The Wrong Trousers (1993) | 4,65 |
| 3 | The Usual Suspects (1995) | 4,48 |
| 4 | Rear Window (1954) | 4,44 |
| 5 | The Shawshank Redemption (1994) | 4,40 |

**Nota:** estas puntuaciones son predicciones del modelo, no calificaciones reales realizadas por el usuario.

---

## 🛠️ 8. Tecnologías utilizadas

| Tecnología | Función |
|:---|:---|
| Python | Lenguaje de programación |
| Google Colab | Entorno de ejecución |
| Pandas | Procesamiento y exploración de datos |
| NetworkX | Construcción y análisis de grafos |
| Matplotlib | Generación de visualizaciones |
| Scikit-Surprise | Implementación de SVD y KNN |
| GridSearchCV | Optimización de hiperparámetros |
| Scikit-learn | Herramientas complementarias |

---

## 📂 9. Estructura del proyecto

El repositorio contiene:

- **Notebook de Jupyter (`.ipynb`):** código completo, explicaciones, gráficas, métricas y recomendaciones.
- **README.md:** documentación y resumen de los resultados.

El notebook incluye el procedimiento para descargar MovieLens 100K y ejecutar el análisis.

---

## ▶️ 10. Cómo ejecutar el proyecto

1. Abrir el archivo `.ipynb` del repositorio.
2. Seleccionar la opción para abrirlo en Google Colab o cargarlo manualmente.
3. En Colab, elegir **Entorno de ejecución → Ejecutar todo**.
4. Esperar a que finalicen la descarga de datos, el análisis de redes y el entrenamiento de modelos.
5. Revisar los resultados, las visualizaciones y las recomendaciones generadas.

**Importante:** algunos procedimientos, especialmente Girvan-Newman y GridSearchCV, pueden requerir varios minutos de ejecución.

---

## ✅ 11. Conclusiones

El desarrollo del proyecto permitió integrar teoría de grafos y sistemas de recomendación en un mismo análisis de datos.

**Principales hallazgos:**

1. MovieLens 100K permitió analizar las interacciones de 943 usuarios con 1.682 películas.
2. El grafo bipartito facilitó la identificación de usuarios activos y películas populares.
3. Girvan-Newman permitió explorar divisiones estructurales en una subred seleccionada.
4. Los modelos SVD y KNN permitieron estimar calificaciones mediante filtrado colaborativo.
5. SVD presentó el menor RMSE en las evaluaciones realizadas.
6. La optimización de hiperparámetros mejoró el desempeño de ambos modelos.
7. El modelo SVD permitió generar cinco recomendaciones personalizadas para un usuario.

### Conclusión general

El proyecto demuestra cómo las técnicas de análisis de redes permiten estudiar las relaciones entre entidades, mientras que los sistemas de recomendación aprovechan los patrones de interacción para generar predicciones personalizadas.

La combinación de estas herramientas constituye una aplicación práctica de la ciencia de datos en el análisis de preferencias y el desarrollo de sistemas inteligentes.

---

**Proyecto académico — Maestría en Ciencia de Datos**

