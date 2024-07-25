# da-prueba-tecnica-transporte

## 1) Realizar un Análisis Exploratorio de Datos (EDA)
#### Antes de comenzar con el EDA, debo de realizar una limpieza inicial de los datos:
#### a) Eliminación de duplicados para evitar sesgos en el análisis.
#### b) Manejo de valores faltantes, detectarlos. Se pueden tratar eliminando filas/columnnas, rellenar con estadístia media o mediana o utilizar técnicas más avanzadas en nuesto caso: 

####    'Numero_Pasajeros lo hemos rellenado con la mediana de la columna, y en 'Duracion_Viajes_minutos primero se convirtieron los datos a numéricos y estos se reemplazaron por la mediana.
#### c) Convesión de tipos de datos, se convirtieron fecha a datetime, Numero_Pasajeros a int, Duracion_Viajes_Minutos a float
#### d) Filtarmos los tipos de transporte inviables.

## 2) EDA a Variables Categórias.
   #### a) Creamos una función para que genere gráfico de barras horizontales para cada columna categórica del Dataframe. La función 'graficos_eda_categoricos' toma como entrada un DataFrame 'cat', que contiene las columnas categóricas que queremos graficar.
   #### b) Importamos la función 'ceil' de la librería 'math' que redondea hacia arriba y cat.shape[1] devuelve el núnero de columnas en el DataFramme 'cat'. 
   #### Entonces el cálculo de filas necearias para los gráficos, se calcula dividiendo el número de columnas entre 2, redondeando hacia arriba con 'ceil'.
   #### c) Luego definimos el gráfico:
   #### f, ax = plt.subplots(nrows = filas, ncols = 2, figsize = (16, filas * 6))
   #### d) Creamnos una figura y una matriz de ejes (ax) con filas y 2 columnas. Con figsize definimos el tamaño de la figura: 16 unidades de ancho y filas * 6 unidades de alto.   
   #### e) Tenemos que aplanar los ejes, ya que ax es una matriz bidimensional de ejes. Utilizamos 'ax.flat', que convierte esta matriz en una vista plana (unidimensional) para facilitar la iteración.
   #### f) Creamos un bucle para añadir gráficos, iterando sobre cada columna en el DataFrame 'cat', usando enumerate para obtener tanto el índice (index) como el nombre de la columna (variable).
   #### g) Con la siguiente línea en el bucle: 'cat[variable].value_counts().plot.barh(ax = ax[index])': 'cat[variable].value_counts()' cuenta la frecuencia de cada categoría en la columna variable.
   ####    .plot.barh(ax = ax[index]) crea un gráfico de barras horizontal de estas frecuencias y lo asigna al eje correspondiente ax[index].
   #### h) Las últimas dos líneas del bucle, una establece el título del gráfico con el nombre de la columna, con tamaño de fuente y negrita, y la segunda ajusta el tamaño de las etiquetas de los ejes.
   #### Se plantean dos opciones para la seleccion de columnas categóricas: cat_df = df.select_dtypes('O') (Selecciona todas las columnas del DataFrame df que son de tipo object.)
   #### cat_columns = df.select_dtypes(include=['object', 'category']).columns  cat_df = df[cat_columns]  (Selecciona los nombres de las columnas que son de tipo object o category.) 
   #### Para trabajar con 'cat_def' la función no debe ser modificada, ya que 'cat' es solo el nombre del parámetro.
   #### Aplicamos la función gráficamente.

## 3) EDA a Variables Numéricas.
   #### a) La función estadisticos_cont toma como entrada un DataFrame num que contiene columnas numéricas.
   #### b) El cálculo de la estadística descriptiva: estadisticos = num.describe().T, num.describe() calcula estadísticas descriptivas básicas (como la cuenta, la media, la desviación estándar, 
   ####    los valores mínimos, los percentiles y los valores máximos) para cada columna en el DataFrame num. 
   ####    .T transpone el resultado para que las estadísticas se presenten como filas y las columnas originales del DataFrame num se presenten como columnas, facilitando la adición de nuevas estadísticas a cada columna.
   #### c) Añadimos la mediana: estadisticos['median'] = num.median(), donde num.median() calcula la mediana para cada columna del DataFrame num.
estadisticos['median'] añade una nueva fila al DataFrame estadisticos con la mediana de cada columna.
   #### d) Se reordenan las columnas: estadisticos = estadisticos.iloc[:, [0, 1, 8, 2, 3, 4, 5, 6, 7]], haciendo que la mediana esté junto a la media. iloc selecciona todas las filas y reordena las columnas especificada por los índices.
   #### e) Se devuelven las estadísticas return estadisticos

## 4) Inconsistencia de Datos
   #### Al tener en cuenta el Tipo_Transporte 'Tranvía' y 'Metro', también los Reatrasos_Minutos de 999,había inconsistencia en los datos, ya que esos dos tipos de transporte no existen para el tipo de rutas que aparecen en los datos, así como esos Retrasos que se ven. Con este filtrado y teniendo en cuenta los tipos de transporte 'Tren' y 'Autobús', graficamos Boxplot y analizamos outliers en Tipo_Transporte
   #### a) Se filtran los outliers de todas las filas donde Retraso_Minutos es igual a 999.
   #### b) Se cuentan los outliers por Tipo_Transporte, se agrupan los datos filtrados por Tipo_Transporte y se cuenta el número de filas por cada grupo.
   #### c) Se identifican las rutas correspondientes, agrupando los datos filtrados por Tipo_Transporte y Ruta , contando el número de filas en cada combinación de grupo.
   #### d) Luego filtramos los retrasos anormalmente altos, eliminando los outliers

## 5) Análisis para merjorar la eficiencia del transporte
   #### a) Análisis de correlación
   ####  * Calculamos  y Analizamos la matriz de correlación
   ####  * Identificamos relaciones significativas entre las variables.
   #### b) Regresión
   ####  * Ajustamos un modelo de regresión para ajustar factores que influyen en la duración del viaje y el retraso.
   ####  * Visualizamos y analizamos los resultados del modelo de regresión
   #### En mi análisis, he obtenido:
   <https://drive.google.com/file/d/1-8sjuYgW6hPPHb88B3qXmOmgf2O5doeK/view?usp=drive_link>
   #### Los valores de p-valor < 0.05 se considera significativo, indicando suficiente evidencia para rechazar la hipótesis nula en caso > 0.05 no se rechaza la hipótesis nula.
   #### El coeficiente para Retraso_Minutos es 0.0465, con un p-valor de 0.076. Esto sugiere que hay alguna evidencia de que los minutos de retraso tienen un efecto positivo en la duración del viaje, aunque el resultado no alcanza el umbral convencional de significancia estadística (p < 0.05). Por lo tanto, este hallazgo debe interpretarse con precaución y podría beneficiarse de estudios adicionales o un mayor tamaño de muestra.

   ### En mi análisis: 
   #### Dia_Semana tiene un p-valor: 0.021
   #### Rechaza la HO.  El día de la semana tiene un efecto significativo en la duración del viaje.

   #### Variables significativas:
   #### - Intercepto, Dia_Semana, 

   #### Variables no significativas
   #### Numero_Pasajeros, Retraso_Minutos (marginalmente significativo), y Tipo_Transporte no son significativamente diferentes de cero. No tienen un efecto significativo en la duración del viaje.

   #### Podrámos hacer un análsis más exautivo para poder interpretar mejor el Retraso_Minutos obteniendo más datos, otras variables, etc.

   ## R-squared
   #### En mi modelo R2 es 0.000, o que indica que el modelo no explica prácticamente nada de la variabilidad en la duración del viaje. Esto sugiere que las variables independientes que estamos usando no son buenas predictoras de la duración del viaje en mi modelo actual.

   #### Luego he realizado el modelo de regresiób con la extracción de características temporales y con varios análisis he llegado a la conclusión que mis variables significativs son Dia_semana y mes. Aquí dejo los datos:
   <https://drive.google.com/file/d/1mqtj-9CmYvszXahO9yXM93wpuh-u-ZGo/view?usp=drive_link>
   #### o sea que tienen algún impacto en la duraciónn del viaje. He debido no hacer uso de algunas de ellas en el análisis por su elevada multicolinealidad.
   #### Vemos un bajo R2 indica que hay factores que tal vez sean importantes y no estar capturados en este modelo, como: condiciones climáticas, datos de tráfico, períodos de vacaciones, etc.
   
   ### c) Análisis de Rutas
   ####  Analizamos el rendimiento de diferentes rutas. Para ello agrupamos los datos por la variable 'Ruta' y calculamos las estadísticas de las variables de interés, usamos gráfficos de barra y gráficos de caja para visualizar los resutlados.








