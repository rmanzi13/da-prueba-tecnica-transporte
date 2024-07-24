# da-prueba-tecnica-transporte

## 1) Realizar un Análisis Exploratorio de Datos (EDA)
### Antes de comenzar con el EDA, debo convertir mis datos al tipo adecuado. Convertiré la fecha que se presenta con Y-M-D H:M:S a Datetiem, Numero_Pasajeros que se preenta como string a int (en este caso
### he tenido que completar los valores NaN con cero para poder realizar la conversion), y Duracion_Viaje_Minutos que se presenta como string a floa. A partir de aqui ya puedo hacer un EDA de los datos. 

## 2) EDA a Variables Categórias.
   ### a) Creamos una función para que genere gráfico de barras horizontales para cada columna categórica del Dataframe. La función 'graficos_eda_categoricos' toma como entrada un DataFrame 'cat',
   ### que contiene las columnas categóricas que queremos graficar.
   ### b) Importamos la función 'ceil' de la librería 'math' que redondea hacia arriba y cat.shape[1] devuelve el núnero de columnas en el DataFramme 'cat'. Entonces el cálculo de filas necearias
   ### para los gráficos, se calcula dividiendo el número de columnas entre 2, redondeando hacia arriba con 'ceil'.
   ### c) Luego definimos el gráfico:
   ### f, ax = plt.subplots(nrows = filas, ncols = 2, figsize = (16, filas * 6))
   ### d) Creamnos una figura y una matriz de ejes (ax) con filas y 2 columnas. Con figsize definimos el tamaño de la figura: 16 unidades de ancho y filas * 6 unidades de alto.
   ### e) Tenemos que aplanar los ejes, ya que ax es una matriz bidimensional de ejes. Utilizamos 'ax.flat', que convierte esta matriz en una vista plana (unidimensional) para facilitar la iteración.


