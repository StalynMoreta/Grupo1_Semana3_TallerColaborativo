# Analisis de Segmentacion de Usuarios Digitales

## Resumen ejecutivo
Aplicamos aprendizaje no supervisado para segmentar usuarios de una plataforma digital de salud.
Implementamos y comparamos K-Means, DBSCAN, PCA y t-SNE sobre el dataset `citaschallenge.xlsx`.
Con este flujo generamos visualizaciones y tablas que nos permiten describir perfiles, contrastar metodos y proponer acciones.

## 1) Objetivo y alcance
El objetivo del proyecto es segmentar perfiles de usuario con tecnicas no supervisadas y comunicar resultados tecnicos de forma clara.
Cubrimos:
- Analisis exploratorio del dataset.
- Limpieza y transformacion de variables.
- Ajuste de K-Means (elbow + silhouette).
- Ajuste de DBSCAN (`eps`, `min_samples`) con busqueda en grilla.
- Visualizacion de resultados y comparacion entre metodos.
- Reduccion de dimensionalidad con PCA y t-SNE.

## 2) Contexto y dataset
Trabajamos con el dataset `Dataset/citaschallenge.xlsx`, que ya fue validado y aceptado por el docente para esta actividad.

Variables principales que usamos en el modelado:
- `GENERO`
- `EDAD`
- `ESTAFINAL`
- `TIPO_AFILIACION`

## 3) Estructura del repositorio
Organizamos el repositorio asi:

```text
Dataset/
  citaschallenge.xlsx
Notebooks/
  Grupo1_semana3.ipynb
Results/
  *.png
  *.csv
README.md
requirements.txt
```

## 4) Reproduccion
Ejecutamos el proyecto asi:

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
jupyter notebook Notebooks/Grupo1_semana3.ipynb
```

Al ejecutar el notebook de inicio a fin, generamos todos los artefactos en `Results/`.

## 5) Metodologia
### 5.1 EDA y limpieza
Revisamos estructura, estadisticos descriptivos, nulos y duplicados.
Transformamos variables categoricas a numericas y estandarizamos el set de entrada para clustering.

Evidencia:
- `Results/visualizacion_distribuciones.png`
- `Results/matriz_correlacion.png`

### 5.2 K-Means
Estimamos el numero de clusters con metodo del codo y metodo de la silueta.
Luego entrenamos un modelo final de K-Means y analizamos sus grupos.
Dejamos una justificacion explicita del `k` final en el notebook, equilibrando calidad estadistica e interpretabilidad.

Evidencia:
- `Results/metodo_codo.png`
- `Results/metodo_silueta.png`
- `Results/segmentacion_kmeans_edad.png`
- `Results/segmentacion_kmeans_afiliacion.png`
- `Results/resumen_clusters_kmeans.csv`

### 5.3 DBSCAN
Hacemos busqueda en grilla de `eps` y `min_samples` y evaluamos:
- cantidad de clusters,
- porcentaje de ruido,
- silhouette score sin ruido.

Con la mejor configuracion, entrenamos DBSCAN final y documentamos clusters y ruido.
Tambien dejamos justificacion explicita del par final (`eps`, `min_samples`) usando tradeoff entre silhouette, numero de clusters y ruido.

Evidencia:
- `Results/dbscan_busqueda_parametros.csv`
- `Results/segmentacion_dbscan_edad.png`
- `Results/segmentacion_dbscan_afiliacion.png`
- `Results/resumen_clusters_dbscan.csv`
- `Results/resumen_clusters_dbscan_sin_ruido.csv`

### 5.4 Comparacion K-Means vs DBSCAN
Comparamos ambos metodos en una vista visual unificada para cumplir el criterio comparativo del enunciado.
Adicionalmente, incluimos analisis critico de fortalezas, limitaciones y escenarios recomendados para cada modelo.

Evidencia:
- `Results/comparativo_kmeans_dbscan.png`

### 5.5 PCA y t-SNE
Usamos PCA para una proyeccion lineal 2D y t-SNE para estructura no lineal.

Evidencia:
- `Results/pca_kmeans.png`
- `Results/tsne_kmeans.png`
- `Results/tsne_genero.png`

## 6) Resultados y conclusiones (ancladas al notebook)
Obtenemos estas conclusiones al ejecutar `Notebooks/Grupo1_semana3.ipynb` y revisar los artefactos que exportamos en `Results/`.

1. Confirmamos que los datos son aptos para clustering despues de limpieza y transformacion.
   Evidencia: `Results/visualizacion_distribuciones.png`, `Results/matriz_correlacion.png`.

2. Identificamos una segmentacion estable con K-Means usando el criterio de codo y silueta.
   Evidencia: `Results/metodo_codo.png`, `Results/metodo_silueta.png`, `Results/resumen_clusters_kmeans.csv`.

3. Observamos que DBSCAN aporta una lectura complementaria al detectar ruido y microgrupos.
   Evidencia: `Results/dbscan_busqueda_parametros.csv`, `Results/resumen_clusters_dbscan.csv`.

4. Comparamos directamente ambos enfoques para interpretar diferencias de estructura y densidad.
   Evidencia: `Results/comparativo_kmeans_dbscan.png`.

5. Validamos visualmente la separacion de perfiles con reduccion de dimensionalidad.
   Evidencia: `Results/pca_kmeans.png`, `Results/tsne_kmeans.png`, `Results/tsne_genero.png`.

6. Construimos perfiles por cluster (K-Means y DBSCAN) con 2-4 lineas por segmento para conectar resultados numericos con decisiones de negocio.
   Evidencia: seccion de perfiles en `Notebooks/Grupo1_semana3.ipynb`, `Results/resumen_clusters_kmeans.csv`, `Results/resumen_clusters_dbscan.csv`.

## 7) Limitaciones y mejoras
- Reconocemos que `ESPECIALIDAD` tiene alta cardinalidad y puede dispersar densidades en DBSCAN.
- Proponemos agrupar especialidades en macro-categorias para una interpretacion mas robusta.
- Proponemos probar escaladores alternativos y evaluar estabilidad de clusters por remuestreo.

## 8) Checklist de entregables
Incluimos en este repositorio:
- Codigo fuente: `Notebooks/Grupo1_semana3.ipynb`.
- Dataset: `Dataset/citaschallenge.xlsx`.
- Documentacion tecnica: `README.md`.
- Visualizaciones y tablas exportadas: `Results/`.

## 9) Dependencias
Fijamos las dependencias en `requirements.txt`, incluyendo `openpyxl` para lectura de Excel con pandas.
