# da-prueba-tecnica-transporte

## 1) Realizar un Análisis Exploratorio de Datos (EDA)
#### Antes de comenzar con el EDA, debo de realizar una limpieza inicial de los datos:
#### a) Eliminación de duplicados para evitar sesgos en el análisis.
#### b) Manejo de valores faltantes, detectarlos. Se pueden tratar eliminando filas/columnnas, rellenar con estadístia media o mediana o utilizar técnicas más avanzadas en nuesto caso: 

####    'Numero_Pasajeros lo hemos rellenado con la mediana de la columna, y en 'Duracion_Viajes_minutos primero se convirtieron los datos a numéricos y estos se reemplazaron por la mediana.
#### c) Convesión de tipos de datos, se convirtieron fecha a datetime, Numero_Pasajeros a int, Duracion_Viajes_Minutos a float
#### d) Filtarmos los tipos de transporte inviables.

## 2) EDA a Variables Categórias.
   #### a) Creamos una función para que genere gráfico de barras horizontales para cada columna categórica del Dataframe. La función 'graficos_eda_categoricos' toma como entrada un DataFrame 'cat', que contiene las columnas categóricas que queremos graficar.  (Explicación de la misma en el jupiter notebook)
   #### Aplicamos la función gráficamente.

## 3) EDA a Variables Numéricas.
   #### La función estadisticos_cont toma como entrada un DataFrame num que contiene columnas numéricas. 
   #### Se devuelven las estadísticas return estadisticos

## 4) Inconsistencia de Datos
   #### Al tener en cuenta el Tipo_Transporte 'Tranvía' y 'Metro', también los Reatrasos_Minutos de 999,había inconsistencia en los datos, ya que esos dos tipos de transporte no existen para el tipo de rutas que aparecen en los datos, así como esos Retrasos que se ven. Con este filtrado y teniendo en cuenta los tipos de transporte 'Tren' y 'Autobús', graficamos Boxplot y analizamos outliers en Tipo_Transporte
   #### a) Se filtran los outliers de todas las filas donde Retraso_Minutos es igual a 999.
   #### b) Se cuentan los outliers por Tipo_Transporte, se agrupan los datos filtrados por Tipo_Transporte y se cuenta el número de filas por cada grupo.
   #### c) Se identifican las rutas correspondientes, agrupando los datos filtrados por Tipo_Transporte y Ruta , contando el número de filas en cada combinación de grupo.
   #### d) Luego filtramos los retrasos anormalmente altos, eliminando los outliers

## 5) Análisis para merjorar la eficiencia del transporte primario
   #### a) Análisis de correlación
   ####  * Calculamos  y Analizamos la matriz de correlación
   ####  * Identificamos relaciones significativas entre las variables.
   #### b) Regresión
   ####  * Ajustamos un modelo de regresión para ajustar factores que influyen en la duración del viaje y el retraso.
   ####  * Visualizamos y analizamos los resultados del modelo de regresión
   #### En mi análisis, he obtenido:
   [Reegresión Primario](https://drive.google.com/file/d/1-8sjuYgW6hPPHb88B3qXmOmgf2O5doeK/view?usp=drive_link).
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
   
## 6) Análisis para mejorar la eficiencia del transporte teniendo en cuenta la extracción de características temporales
   #### Luego he realizado el modelo de regresión con la extracción de características temporales y con varios análisis he llegado a la conclusión que mis variables significativs son Dia_semana y mes. Aquí dejo los datos:
   [Regresión con Extracción características termporales](https://drive.google.com/file/d/1mqtj-9CmYvszXahO9yXM93wpuh-u-ZGo/view?usp=drive_link)
   #### o sea que tienen algún impacto en la duraciónn del viaje. He debido no hacer uso de algunas de ellas en el análisis por su elevada multicolinealidad.
   #### Vemos un bajo R2 indica que hay factores que tal vez sean importantes y no estar capturados en este modelo, como: condiciones climáticas, datos de tráfico, períodos de vacaciones, etc.
   
   ### c) Análisis de Rutas
   ####  Analizamos el rendimiento de diferentes rutas. Para ello agrupamos los datos por la variable 'Ruta' y calculamos las estadísticas de las variables de interés, usamos gráfficos de barra y gráficos de caja para visualizar los resutlados.
[Gráficos](https://colab.research.google.com/drive/1TOkospjxZfEpClZLN3qY2-kR9QcC_575?authuser=1#scrollTo=TlBp6wNBiZo7)

## 7) Diseño de Base de Datos en SQL e Inserción de Datos usando Python
   #### Para ello he obtenido el archivo luego de la limpieza del archivo original, usando la columna fechan con todos los datos de fecha y tiempo, ya que es más simple de mantener y almacernar  utiliza menos espacio de almacenamiento. De esta manera se mantiene la simplicidad e integridad de los datos, y siempre se pueden crear índices y utilizar funciones de fecha y tiempo para extraer datos específicos en mis consultas.
   [Datos para BD](https://colab.research.google.com/drive/14JiNQ2BVn5h2Sg6JZTE-cqsmWjOmGVBd?authuser=1#scrollTo=WdW17AfKMDd8)





