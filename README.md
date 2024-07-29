# da-prueba-tecnica-transporte

## 1) Realizar un Análisis Exploratorio de Datos (EDA)
#### Antes de comenzar con el EDA, debo de realizar una limpieza inicial de los datos:
#### a) Eliminación de duplicados para evitar sesgos en el análisis.
#### b) Manejo de valores faltantes, detectarlos. Se pueden tratar eliminando filas/columnnas, rellenar con estadístia media o mediana o utilizar técnicas más avanzadas en nuesto caso: 

####    'Numero_Pasajeros lo hemos rellenado con la mediana de la columna, y en 'Duracion_Viajes_minutos primero se convirtieron los datos a numéricos y estos se reemplazaron por la mediana.
#### c) Convesión de tipos de datos, se convirtieron fecha a datetime, Numero_Pasajeros a int, Duracion_Viajes_Minutos a float
#### d) Coincidencia de Regiones. Definimos la ciudades, creamos la función para verificar coincidencia. la aplicamos para filtrar los datos.
#### e) Filtarmos los tipos de transporte inviables.

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
   [Reegresión Primario](https://drive.google.com/file/d/1IZ8ELI-nskO3oTl-T67eMEUyrKcn47SO/view?usp=drive_link).
   #### Los valores de p-valor < 0.05 se considera significativo, indicando suficiente evidencia para rechazar la hipótesis nula en caso > 0.05 no se rechaza la hipótesis nula.
   #### R2 y R2 ajustado indican que el modelo no explica la variabilidad en la duración del viaje. Además, la prueba F sugiere que las variables independientes no son predictivas de la duración del viaje.
   #### Podríamos hacer un análsis más exautivo para poder interpretar mejor el Retraso_Minutos obteniendo más datos, otras variables, etc.

## 6) Análisis para mejorar la eficiencia del transporte teniendo en cuenta la extracción de características temporales
   #### Luego he realizado el modelo de regresión con la extracción de características temporales y con varios análisis he llegado a la conclusión que el modelo no es significativo, igual que el análisis anteriior, y que ninguno de los coeficientes de las variables independientes es estadísticamente significativo no tienen un impacto claro en Duración del Viaje.
   [Regresión con Extracción características termporales](https://drive.google.com/file/d/1bFdelJgwQBfd0gPKyeRURN-_WFC-BQ9d/view?usp=drive_link)
   #### Podría haber factores que tal vez sean importantes y no estar capturados en este modelo, como: condiciones climáticas, datos de tráfico, períodos de vacaciones, etc.

   #### He probado utilizando Retraso_Minutos como variable independiente y no muestra cambios significativos.
   
   ### c) Análisis de Rutas
   ####  Analizamos el rendimiento de diferentes rutas. Para ello agrupamos los datos por la variable 'Ruta' y calculamos las estadísticas de las variables de interés, usamos gráfficos de barra y gráficos de caja para visualizar los resutlados.
[Gráficos](https://colab.research.google.com/drive/1tJFdJccrAydKX48Y0pc1dnjoabW_IrLH?authuser=1#scrollTo=d3Zs01NxWJI5)

## 7) Creación Base de Datos
   #### a) Cargamos el DataFramme con los datos finales
   #### b) Creamos la base de datos y la conectamos a una base de datos SQLite llamada transporte_publico.db
   #### c) Creamos la tabla 'transporte_publico' con las columnas necesarias
   #### d) Preparamos los datos para la inserción: seleccionamos las columnas que queremos insertar y las convertimos a una lista de listas
   #### e) Insertamos los datos utilizando 'executemany' para insertar todos los datos en la tabla.
   #### f) Confirmamos los datos con commit y cerramos la conexión.

[BD_Python_SQL](https://colab.research.google.com/drive/1_gTev18pvVn_LSx4nHNSlQwyNlOTOkX1?authuser=1)

## 8) Creación del Dashboard con Power BI que incluya las principales conclusiones de mi análisis. 
   #### Hemos realizado un análisis con diferentes gráficos para poder visualizar el promedio de la Duración del viaje en minutos por Rutas, así como el promedio del Retraso por Tipo de Transporte. Tambien se crearon dos visualizaciones para poder ver la duración y el retraso a lo largo del tiempo.
   #### Se utilizaron diferentes slicer para poder filtrar los datos por diferentes dimensiones como: Dia Semana, Mes, Ruta, Tipo Transporte.
   #### Se incluyeron tarjetas de resumen, que muestran KPIs importantes como: promedio de duración del viaje, promedio de retraso y número total de viajes.
   #### Para los dos primeros KPIs he utilizado la tarjeta, ya que mostraré un valor único en este caso. Si tuviera más información podría utilizar visualziación KPI para mostrar la tendencia de este valor a lo largo del tiempo y compararlo con un objetivo (target). Con los datos que tengo, son solo 3 meses por eso he decidido utilizar la tarjeta con un valor único.
   #### Para las visualizaciones KPI podría crear medidas, siendo mi objetivo un valor fijo, por ejemplo para la duración del viaje, poddría ser 200 minutos, esta medida sería: 'Objetivo_Duracion_Viaje = 200'
   #### También podríamos crer una medida de objetivos variables, que mi objeetivo para la duración varíe según diferentes rutas, siendo una medida más compleja.
   #### Para crear el KPI del número total de viajes, al no tener una columna específica, creamos una medida que cuente el número de registros en mi tabla, ya que cada registro es un viaje. En marzo vemos menos viajes ya que solo tenemos datos hasta el 11 de marzo.
   

## 9) Conclusiones del Dashboard.
   #### Debemos tener en cuenta la poca cantidad de datos que tenemos, por lo tanto estos resultados pueden estar sesgados.
   #### La larga duración de los viajes, podría estar relacionada con la duración de las rutas, frecuencia de paradas, las condiciones del tráfico y la ruta.
   #### El retraso parece elevado, sugiriendo problmas de puntualidad en los viajes y posibles interrupciones en la ruta. 
   #### Debemos tener en cuenta que no tenemos muchos datos, y que estos patrones pueden cambiar con datos adicionales.

[Dashboard](https://drive.google.com/file/d/1yZHe-MNH-Iis8-YXSnP55OL5nwqjM0r1/view?usp=drive_link)
      

   



   
