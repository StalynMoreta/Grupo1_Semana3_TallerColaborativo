Análisis de Segmentación de Usuarios Digitales

1. Preparación del Entorno
Para el desarrollo de este proyecto se configuró un entorno de análisis de datos en Python, a continuación el detalle técnico:

- Tecnologías y Librerías: Lenguaje: Python 3.x.
- Manipulación de Datos: pandas, numpy.
- Modelado No Supervisado: scikit-learn para desarrollar los modelos: KMeans, DBSCAN, PCA, TSNE.
- Visualización: matplotlib, seaborn.
- Métricas: silhouette_score.

2. Selección y Carga del Dataset
Se utilizó el dataset "citaschallenge", el cual contiene registros de citas médicas de una plataforma digital con las siguientes variables clave:

- Demográficas: GENERO, EDAD.
- Operativas: ESPECIALIDAD, FECHA_CITA, ESTAFINAL.
- Negocio: TIPO_AFILIACION (Convenio, Silver, Gold).

3. Análisis Exploratorio de Datos (EDA) y Preprocesamiento
El análisis estadístico arrojó la siguiente información:
- Registros: 67,650 entradas sin valores nulos ni duplicados detectados.
- Distribución de Edad: El promedio de edad es de 38.7 años, con una desviación estándar de 14.5, con un rango identificado que va de 0 a 96 años.

- Variables Categóricas: Se identificaron tendencias en la afiliación, con más datos en los niveles Silver y Gold.
- Transformaciones Realizadas
    - Encoding: Las variables categóricas fueron convertidas a formato numérico para ser procesadas por los algoritmos:
      GENERO: Femenino (0), Masculino (1).
      TIPO_AFILIACION: Convenio (1), Silver (2), Gold (3).
- Normalización: Se aplicó StandardScaler para asegurar que variables con diferentes escalas (como la Edad frente al Género) tengan el mismo peso en el cálculo de distancias.

4. Implementación de Modelos y Justificación Técnica
K-Means
- Justificación: Elegido por su eficiencia en datasets grandes para crear grupos basados en centroides.
- Metodología: Se utilizó el Método del Codo y el Análisis de Silueta para definir el número óptimo de clusters.
- Hallazgo: Se determinaron clusters bien definidos que separan a los usuarios principalmente por nivel socioeconómico con la variable Afiliación y ciclo de vida con la variable Edad.

DBSCAN
- Justificación: A diferencia de K-means, DBSCAN permite identificar formas de clusters irregulares y detectar outliers (ruido) que no encajan en ningún perfil estándar.
- Ajuste: Se calibraron los parámetros eps y min_samples para encontrar densidades de comportamiento significativas en el uso de especialidades médicas.

Reducción de Dimensionalidad: PCA vs. t-SNE
PCA: Utilizado para reducir la complejidad lineal y visualizar la separación global de los clusters en 2D.
t-SNE: Aplicado para capturar relaciones no lineales. Esta técnica permitió visualizar grupos de usuarios con comportamientos muy específicos que el PCA pasaba por alto.

5. Análisis de Resultados y Perfiles Identificados
Tras agrupar los datos por clúster y analizar sus medias, se identificaron los siguientes perfiles representativos:

- Perfil Ejecutivo (Cluster Gold/Silver - Adulto): Usuarios de 35-50 años con afiliaciones de alto nivel, alta tasa de cumplimiento de citas.
- Perfil Familiar (Cluster Mixto - Joven/Niños): Segmento de menor edad con afiliaciones tipo convenio con especialidades como pediatría u odontología.
- Perfil Senior (Cluster Especializado): Usuarios mayores de 60 años concentrados en especialidades específicas como cardiología o medicina interna.

6. Reflexiones y Conclusiones
Diferencias Clave
- K-means proporcionó una segmentación visualmente más sencilla y fácil de interpretar para identificar los objetivos de mercado.
- DBSCAN reveló que hay un grupo de usuarios con comportamientos erráticos que podrían representar ruido o errores de sistema.

Limitaciones y soluciones propuestas
- Limitación: La variable ESPECIALIDAD tiene demasiadas categorías únicas, lo que dispersa la densidad en DBSCAN.
- Solución propuesta: Realizar una agrupación de especialidades en categorías generales (Ej: Quirúrgicas, Diagnósticas, Consultas Generales) para mejorar el rendimiento del modelo.

Recomendación de Negocio
Se recomienda adaptar la comunicación de la plataforma:
- Notifications personalizadas para el "Perfil Senior" sobre chequeos preventivos.
- Campañas de upgrade de afiliación para el "Perfil Ejecutivo" basadas en su alta frecuencia de uso.
