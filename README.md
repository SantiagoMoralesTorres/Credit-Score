# Credit Score

## Sobre la Base de Datos
La base de datos corresponde al registro de las características demográficas y bancarias de los clientes de un banco, donde cada fila representa un registro mensual por cliente. En total, se tienen 100,000 registros correspondientes a los meses de Enero a Agosto de 12,500 clientes, y un total de 28 variables. En particular, la variable objetivo de este proyecto es Credit Score, la cual resume el comportamiento del cliente respecto a sus cuentas, transacciones, inversiones, préstamos y deudas, además de dar un indicio del riesgo de inclumplimiento de pago en un futuro, y se clasifica en 3 categorías: Good, Standard y Poor.

## Objetivos
* Limpieza y transformación de los datos para mantener la consistencia en la base de datos. 
* Encontrar relaciones importantes entre las variables de la base y Credit Score.
* Analizar que tan distinguibles o separables son los niveles de Credit Score mediante algoritmos de Aprendizaje No Supervisado.
* Encontrar un modelo de Aprendizaje Supervisado que nos permita predecir con un Accuracy elevado a Credit Score.

## Metodología
* La base de datos contenía errores como NA's y espacios en blanco, datos mal capturados (simbolos extra como #$%), outliers y datos sin sentidos. Dado que la base de datos contenía información de un mismo cliente cada 8 registros, se agruparon los datos por clientes para corregir estos valores usando la moda para variables categóricas y la mediana para variables de tipo numérica del cliente por variable. También se realizaron las conversiones del tipo de variable que realmente correspondía.
* Se realizó un análisis descriptivo de los datos para encontrar patrones de las variables de la base de datos con respecto a la variable Credit Score. Se utilizaron gráficos tipo boxplot para las variables numéricas y gráficos de columnas 100% apiladas para las variables categóricas, teniendo en cada gráfico la variable de interés agrupada con los 3 niveles de Credit Score (Good, Standard, Poor).
* Se aplicaron técnicas de reducción de dimensión como Ánalisis de componentes principales para visualizar en 2 dimensiones las relaciones entre las variables de la base de datos y Credit Score, además de visualizar el agrupamiento de cada uno de los 3 niveles de Credit Score. Adicionalmente, se aplicaron técnicas de agrupamiento como K-Means y Métodos Jerárquicos para visualizar que tan distinguibles eran los 3 niveles de Credit Score.
* Finlamente, se realizó el entrenamiento y evaluación de muchos modelos de aprendizaje supervisado como Regresión Logística, LDA, QDA, Naive Classifier, K Nearest Neighbors, Árbol de Decisión, Bosque Aleatorio, Extreme Gradient Boosting, y un Stacking de los 3 mejores modelos. Para cada modelo, se hizo la evaluación considerando 5 Cross Validation, y durante el entrenamiento, se realizó el tuneo de los hiperparámetros correspondientes con 3 Cross Validation. 

## Resultados
Se encontró que aquellos con puntuación crediticia Good poseen una edad avanzada, historial credicitio muy antiguo, y una posición económica alta, la cual se refleja en ingresos altos, mayor inversión y balances mensuales altos en sus cuentas. Por otro lado, aquellos con puntuación crediticia Bad denotaron un comportamiento irresponsable respecto a sus préstamos y créditos, ya que se destacaban por tener muchos préstamos, deudas altas, muchas tarjetas de crédito y cuentas de banco, tasas de interés altas, retrasos en sus pagos y muchos pagos mínimos.

Los métodos de aprendizaje no supervisado como PCA, K-Means y Método Jerárquico, lograron identificar patrones de agrupación de las 3 clases de Credit Score (Good, Standard y Poor), aunque también se observó que existen muchas observaciones de una clase que comparten características muy similares de otra clase, sobre todo entre las clases Good y Poor, donde muchas observaciones de la clase Poor comparten similtudes con las observaciones de la clase Good, lo cual no ocurre tanto de manera inversa, y por tanto, podría interferir en la predicción.

En el caso de la predicción, partiendo del baseline de 53% de Accuracy, correspondiente a clasificar a todos con una puntuación crediticia "Standard" (clase de mayor proporción), los modelos de aprendizaje supervisado alcanzaron un Accuracy desde 61%-66% con Regresión Logística, LDA, QDA, y Naive Classifier, aumentando a 73%-78% de Accuracy con KNN, Árboles de Decisión y Extreme Gradient Boosting, y obteniendo hasta 81% de Accuracy con Random Forest. Se equilibraron también métricas como el Recall de la clase Poor y Precision de la clase Good, obteniendo valores de hasta 84% y 77% respectivamente con Random Forest, esto con el objetivo de disminuir tanto la clasificación incorrecta de aquellos de la clase Poor, como la clasificación con la etiqueta "Good" a aquellos de la clase "Poor", ya que estos son los errores de clasificación más costosos para el banco.

## Sobre los archivos del repositorio

| Archivo                                     | Descripción                                               |
|---------------------------------------------|-----------------------------------------------------------|
| `codigo/Credit_Score.Rmd`                   | Código fuente en R Markdown                               |
| `codigo/metricas/metricas generales`        | Métricas generales (`.rds`) por modelo                    |
| `codigo/metricas/metricas por clase`        | Métricas por clase (`.rds`) por modelo                    |
| `dashboards/Credit Score.pbix`              | Dashboard en Power BI                                     |
| `dashboards/Credit Score.twb`               | Dashboard en Tableau                                      |
| `datos/datos.csv`                           | Dataset original en formato `.csv`                        |
| `datos/datos_limpios.xlsx`                  | Dataset limpio transformado en `.xlsx`                    |
| `reporte/Credit_Score.pdf`                  | Reporte final detallado del proyecto     

## Consideraciones adicionales
Con el objetivo de evitar tiempos prolongados de ejecución (que pueden ser de varias horas), los resultados de evaluación de cada modelo se han guardado previamente en archivos `.rds`. Estos archivos están ubicados en las carpetas codigo/metricas. Para ejecutar el código correctamente, será necesario **modificar las rutas locales de carga de archivos** en el script, tanto para los archivos `.rds` como para el archivo `.csv`, según la ubicación en el equipo del usuario de estos archivos.

En la vista previa de GitHub, algunas páginas del reporte Credit_Score.pdf pueden mostrarse repetidas por un error del visor web. Al descargar el archivo, el reporte se visualiza correctamente.
