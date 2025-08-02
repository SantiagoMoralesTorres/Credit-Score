# Credit Score

## Sobre la Base de Datos
La base de datos corresponde al registro de las características demográficas y bancarias de los clientes de un banco, donde cada fila representa un registro mensual por cliente. En total, se tienen 100,000 registros correspondientes a los meses de Enero a Agosto de 12,500 clientes, y un total de 28 variables. En particular, la variable objetivo de este proyecto es Credit Score, la cual resume el comportamiento del cliente respecto a sus cuentas, transacciones, inversiones, préstamos y deudas, además de dar un indicio del riesgo de inclumplimiento de pago en un futuro, y se clasifica en 3 categorías: Good, Standard y Poor.

## Objetivos
* Limpieza y transformación de los datos para mantener la consistencia en la base de datos. 
* Encontrar relaciones importantes entre las variables de la base y Credit Score.
* Analizar que tan distinguibles o separables son los niveles de Credit Score mediante algoritmos de Aprendizaje No Supervisado.
* Encontrar un modelo de Aprendizaje Supervisado que nos permita predecir con un Accuracy elevado a Credit Score.

## Resultados principales
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
Con el objetivo de evitar tiempos prolongados de ejecución (que pueden ser de varias horas), los resultados de evaluación de cada modelo se han guardado previamente en archivos `.rds`. Estos archivos están ubicados en las carpetas codigo > metricas > metricas generales/por clase. Para ejecutar el código correctamente, será necesario **modificar las rutas locales de carga de archivos** en el script, tanto para los archivos `.rds` como para el archivo `.csv`, según la ubicación en el equipo del usuario de estos archivos.
