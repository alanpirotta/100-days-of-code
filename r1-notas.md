**Comienzo este archivo en el día 44. Me pareció una buena forma de rastrear el proceso, tomar notas y poder encontrarlas después**

### hotkeys jupyter notebook
* esc/enter: entrar y salir de modos
* Y/M: convertir celda en code/markdown
* A/B: insertar celda arriba/abajo
* D D: borrar una celda
* X/C/V: Cortar, copiar y pegar celdas seleccionadas
* ctrl + /: Comentar una línea

### R1D44
*pandas en kaggle*
- DataFrame.apply: sirve para modificar todos los valores en u n DF. el "axis" es para definir si lo hace en cada columna o en cada fila.
- DataFrame.groupby([columna]): Agrupa todas las filas con el mismo valor. (símil a tablas dinámicas en excel)
- DataFrma.groupby().size(): Devuelve una series con la cantidad de entradas de cada agrupación.
- sort_values(): si es una series no necesita "by=", si es un DF requiere que se seleccione la columna.

### R1D45
*pandas en kaggle*
- dtype (columnas/series) y dtypes (df)
- astype: sirve para cambiar el tipo de dato (crea nueva serie)
- pd.isnull y pd.notnull
- fillna y replace: Para reemplazar valores de los DF y series.
- Practica de df.shape, df.count(), df.column.value_counts, groupby para series (si se pone el nombre de la serie dentro del groupby, agrupa por los valores)
- df.rename(): sirve para renombrar index o nombres de columnas. 
ejemplo: df.rename(columns={'antiguo_nombre': 'nuevo_nombre'})
- df.rename_axis(): renombrar los "ejes" de la tabla. 
ej: df.rename_axis('nombre_columnas', axis='columns')
- pd.concat([df1, df2]): une los dos DF en uno solo (tendría que tener las mismas columnas)
- df.set_index(): setea los index usando una o más columnas del DF. Sirve para después juntar varios DF usando estas columnas como puntos en común.
- df.join(): junta dos DF en uno. Las columnas deben tener distintos nombres ( o agregar sufijos)

### R1D46

*data visualization en kaggle con seaborn*
Matplotlib(plt): Sirve para definir las características del gráfico (no el contenico?) 
- plt.figure(figsize=(ancho,alto)): Define el tamaño del gráfico
- plt.title("Título del gráfico")
- plt.xlabel("etiqueta eje X")

- sns.lineplot(data=DataFrame): gráfico de linea. Puedo definir varias columnas sólas en diferentes lineas, seleciconando DataFrama['columna'] (agregar atributo "label=")

### R1D49

- DF.max(axis=1)['row']: Para buscar el máximo valor de una fila (si se cambia el axis sería de una columna)
- DF.idxmin(axis=1)['row']: Para buscar el nombre de la columna donde está el mínimo. se puede cambiar para buscar el indice de la fila 
- DF.max().idxmax(): Devuelve el label de la columna con el valor más alto de un DF
- DF[DF.max().idxmax()].idxmax(): devuelve el index del valor más alto de un DF

- plt.xticks(rotation=90): Sirve para rotar 90 grados las label del eje X. busqué si podía hacerlo con plt.xlabel pero me parece que no existe


- sns.barplot(x= ,y= ): Gráfico de barras
- sns.heatmap(data= DF, annot=True): Gráfico de calor. el annot es para que muestre los valores de cada comparación
- sns.scatterplot(x= , y= ): Gráfico scatter. Sirve para ver correlación. Se puede hacer con una regresión
- sns.regplot(x= , y= ): gráfico scatter con regresión lineal.
- sns.lmplot(x= "nombre columna", y= "nombre columna", hue= "nombre columna" , data= df): Gráfico de regresión con dos rectas, uno por cada set (color-coded con el "hue")
- sns.swarmplot(x= , y= ): categorical scatter plot. Sirve cuando el X es un booleano por ejemplo

### R1D50
- Acceder a un valor de una fila y columna:
    - df.loc[][]: df.loc[ valor del índice ][columna]. 
    - df.at[índice, columna]: Devuelve sólo un valor 
    - df.loc[][]: df.loc[ df.index == ][ columna].values[0]. obtiene una series, la convierte a ndarray con values y muestra el indice 0. Esta forma es porque al tener una condición, el loc puede tener más de un valor y por eso trae una series.

- plt.legend(): Llamarlo antes del plt.show() para que muestre los label de los gráficos (si se definieron dentro del gráfico, el () queda vacío acá)

- sns.distplot(a= "columna del DF para eje x", kde=False, label=): el kde genera un histograma de densidad en vez de valores (fuera del valor del eje y, no estoy 100% seguro de en que se diferencia) 
*Deprecado*
- sns.histplot o snsdisplot se usan ahora (los datos se cargan con data=)
- sns.kdeplot(data= "columna del DF para eje x", shade= (boolean colorear area debajo), label=): Es un histograma donde te suaviza todo y unifica, en vez de ser barras por valor.
- sns.jointplot(x= , y= , kind="kde"): Te une dos gráficos kde, y los muestra "desde arriba"
- sns.set_style("theme"): Cambia el estilo de los gráficos a uno de los 5 temas: (1)"darkgrid", (2)"whitegrid", (3)"dark", (4)"white", and (5)"ticks"


