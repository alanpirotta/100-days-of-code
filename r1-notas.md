**Comienzo este archivo en el día 44. Me pareció una buena forma de rastrear el proceso, tomar notas y poder encontrarlas después**

### A averiguar
*librería from pathlib import Path*
Tengo que averiguar bien que significa cuando pongo "add ." en git y me tira esto:
*LF will be replaced by CRLF in ...* 
*The file will have its original line endings in your working directory*

### Pendientes
* Averigar como poner las labels del eje x a 45° en subplots de seaborn

### hotkeys jupyter notebook
* esc/enter: entrar y salir de modos
* Y/M: convertir celda en code/markdown
* A/B: insertar celda arriba/abajo
* D D: borrar una celda
* X/C/V: Cortar, copiar y pegar celdas seleccionadas
* ctrl + /: Comentar una línea

### Orden útil de análisis de datos:
- Read_csv o equivalente con todos los datos para tener un buen df. graficos simples, describe e info para ver como se comportan los datos
- Buscar y rellenar/vaciar valores vacíos. Se pueden rellenar con 0, mean, median, ffill o bfill. También pueden pedirse si es muy importante, o averiguar por qué ocurrió si es un conjunto grande de datos. 
- Buscar errores en valores: valores fuera de rango, duplicados. También usar métodos de str, dt y cat segun tipo de columna.
- Graficacion de datos más complejos con los datos limpios.
- Conclusiones.
- Estética del informe.

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

- plt.xticks(rotation=90): Sirve para rotar 90 grados las label del eje X y dejarlas en vertical (45 también queda bien) . busqué si podía hacerlo con plt.xlabel pero me parece que no existe


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

### R1D52

- pd.to_numeric(): sirve para convertir una series a int o float. Para convertir parte de un df, se puede usar appliy:
    - df[['column1', 'column2']].apply(pd.to_numeric, errors=, downcast=): el errors sirve para que los no convertibles los ignore o los convierte en NaN. downcast te devuelve el int o float más chico posible
- df.astype(int/float): Convierte el tipo de las columnas al buscado. No acepta NaN, por lo que se debe usar fillna() antes.
- df.rename(columns={'nombreviejo': 'nombrenuevo'}): Sirve para cambiar nombres de columnas a otros
- df[['columna1', 'columna2']]= df['columna a dividir'].str.split('caracter que divide', expand=True): Para separar una columna en más de una, según un caracter. el expand=True es para que directamente lo divida en diferentes columnas.
- df.drop('columna/fila', inplace=, axis=): Para eliminar una columna/fila. inplace=True sobreescribe el archivo, es preferible guardarlo de nuevo. 
- df.info(): te muestra varios datos, sirve para ver la cantidad de valores NaN de cada columna. Alternativa: df.isna().sum()
- df[ df['columna'].isna() ]: Sirve para chequear todas las filas en las que no hay datos para esa columna
- df[una series].str.replace('valorviejo', 'valornuevo'): Sirve para reemplazar una parte de string en una columna

### R1D53 y 54

Formas de separar un df por años, cuando la columna es una fecha completa
- df_2017 = df['2017-01-01':'2017-12-31']: forma completamente manual, funciona pero se hace una línea por año
- datos_2018 = datos['{}-01-01'.format('2018'):'{}-12-31'.format('2018')]: Funciona para hacer un ciclo
- Lo siguiente devuelve una lista de dataframespor año:
años=[2017,2018,2019,2020,2021]
años_df=[]
for año in años:
    años_df.append(datos['{}-01-01'.format(año):'{}-12-31'.format(año)])

- datos.index.date[0]: Devuelve datetime.date(año, mes, dia) de la primer fila. Es un tipo de dato "datetime.date"
    Si agrego .year devuelve el año, pero de esa fila específica. Tendría que hacer un loop por todos los indices del objeto datetime


- pd.set_option('display.max_rows', 10): Sirve para el display de un máximo de filas al poner "df"

### R1D55

- df = df.reset_index(): Resetea el index y lo convierte en una columna.
- df = df.set_index('feature'): Poner una columna como index. Sirve para volver a poner luego de resetear
- df['mes_año'] = df['Fecha'].dt.to_period('M'): Extrae el mes y año y los crea en una nueva columna. si se pone 'Y' extrae solo el año.
- df['año'] = pd.DatetimeIndex(df.index).year: Crea una columna con sólo el año de la fecha que está como index
- Error "'DatetimeIndex' object has no attribute 'dt'" lo tira cuando se quiere usar el index para el to_period. Tiene que ser una serie si o si (feature del df)
- df['mes_dia']= df['Fecha'].dt.strftime('%m-%d'): Sirve para extraer como un string el mes y día solamente de una fecha. NO se puede considerar como fecha sin el año.

- Para graficar varios graficos con una celda, se puede poner el código del primer gráfico, después un plt.show(), después el siguiente código, otro plt.show()... etc
- fig, axs = plt.subplots(nfilas, n°col, figsize=(16,10)): Para crear varios gráfico en la misma celda, sin separación. **no logré averiguar bien como rotar 45° las label del eje x**

#### Falta averiguar la próxima vez, como encontrar índices duplicados, el DF del 2020 me tira error por eso. Con años_df[2020].index.is_unique lo confirmo, y dice False

### R1D56

Chequeo de duplicados en index. (aplica para columnas que no sean índice)
- df.index.duplicated(): Devuelve un array con True para la segunda aparición de un valor. Si se pone keep='last', el que mantiene (aparece como False) es la última aparición. Si se pone keep=False devuelve con True en todos los valores duplicados. 
- df = df.drop_duplicates(): Descarta todos los valores duplicados.
- ((array1 == array2) == False).sum(): Sirve para chequear que todas las columnas de la fila duplicada (cada array) sean iguales o no. Se puede también comparar directo con un loc, pero si el repetido es el índice, antes se debe resetear el índice.

- variable = [i**2 for i in range(10)]: ejemplo de forma de escribir un loop en una línea (list comprehension)
- df['año_mes'] = df[columna con fecha].dt.to_period('M'): Extrae sólo el año y día. Si la fecha es en el índice, primero resetear

Quedé en que puedo agrupar por año_mes (o multindex con columnas año y mes), para obtener todos los datos de promedios

### R1D57

- df_nuevo = df.reset_index().set_index(['columna_1', 'columna_2']): indexar dos columnas del dataframe (o más) como multiIndex.
- df_nuevo.loc[(dato_primer_index , dato_segundo_index)]: Esto sirve para acceder a un dato específico (o conjunto de datos), de un df con multiIndex.
- Genera un df nuevo con datosespecíficos de cada columna luego de un groupby
  gb = df.groupby(['col1', 'col2'])
  counts = gb.size().to_frame(name='counts')
  (counts
   .join(gb.agg({'col3': 'mean'}).rename(columns={'col3': 'col3_mean'}))
   .join(gb.agg({'col4': 'median'}).rename(columns={'col4': 'col4_median'}))
   .join(gb.agg({'col4': 'min'}).rename(columns={'col4': 'col4_min'}))
   .reset_index()
  )
- df.groupby(['A', 'B'])['C'].describe(): Alternativa y te muestra las de una columna sola
- Para agregar una columna de suma de datos en un multiIndex de columnas (el condicional es para eliminar las columnas que no sean numéricas, que NO se quieran agregar):
    for columna in por_mes.columns:
        if columna == 'Fecha':
            continue
        agrupado_por_mes[columna,'sum'] = por_mes.groupby(['año','mes'])[columna].sum()
- d.columns = d.columns.map('_'.join): Para unir si tiene multiIndex en columnas, te une en un sólo índice


### R1D58

- df.loc[(indice_1_nivel,indice_2_nivel),'columna'] = value : Esto sirve para cambiar un valor. (puede ser que cambie varios si comparten esos índices)
- df.groupby('columna1').describe().loc[indice,'columna2'] : Agrupa, muestra los datos descriptivos de una parte específica.
- df.groupby('columna1').agg(['count', 'sum', 'mean', 'median']).loc[índice,'columna2']: Otra forma de obtener lo mismo, pero con el método agg donde puedo seleccionar qué quiero poner, y poner otras cosas (como la suma)


  
### R1D59

- https://www.colourlovers.com/palettes/ :  Esta página sirve para buscar paletas de colores (útiles para los gráficos)
- df.index.get_level_values(nivel de indice(0,1,2...)).unique(): Para extraer los valoresúnicos de un índice específico. Forma extraña, hay más fáciles.
- df.loc[(indice1, )].index: forma de extraer los valores del segundo índice, de un sólo valor del primer índice
- df.loc[(índice1, )]['indice_col1']['indice_col2']: Forma de acceder a una columna específica cuando se tiene multiIndex en filas Y columnas. Se puede poner también como ['indice_col1', 'indice_col2']
- plt.legend(fontsize= 'large'): tamaño de la letra en la leyenda
- df.columns = ['_'.join(col).strip('_') for col in df.columns.values]: Sirve para unir los nombres de las columnas, con un guión bajo en el medio y eliminandolo al final si no tiene segundo Indice

### R1D60

- Df.fillna(method='ffill') o bfill: para que conplete los NaN con el valor de la fila anterior.
- read_csv(data,
           dtype='', : Se puede definir los tipos de datos directamente, ingresando como un diccionario con las colmnas como keys.
           skip_blank_lines=True : Eliminar las filas que no tienen datos (generalmente al inicio o al final)
- array.tolist(): Convierte un array a una lista.

### R1D61

- df.drop(df[<some boolean condition>].index): Eliminar filas según una condición o valor. La condición puede ser un df filtrado
- Formas de medir la cantidad de filas:
    - df.count()
    - df.shape[0]
    - len (df)

### R1D62

- np.around('numero',cantidaddedecimales): Redondea el numero a la cantidad de decimales pedidos (me sirvió mucho al calcular la media de columnas)
- pd.DataFrame(data): Para crear un DataFrame, primero crear un diccionario con las diferentes columnas (los valores pueden ser series, o listas por ejemplo)
- df.sort_values(by=['columna'], ascending=False): Ordena de mayor a menor (crea nuevo df)
- df['columna'].replace({valoranterior:valornuevo, valoranterior2:valornuevo2}): Sintaxis que sirve para modificar varios valores por otros en una columna de un df. Genera un nuevo df
- pd.melt(data, id_vars= ['columna que se quiere mantener], value_vars=['columnas que se quieren ubicar una encima de la otra]): Converte todas las columnas a sólo dos: variable ( nombre de columna) y value ( valor ). Sirve para graficar más de dos columnas facilmente por ejemplo
- sns.catplot(kind='count', hue='', col=''): el kinddefine que uno de los ejes será la suma de ocurrencias del otro. Con hue='' se puede dividir más y en colores. con col=, genera dos o más subplots. **este es un gráfico que funciona a nivel figura, porque lo que no se puede hacer subplot con mpl**

### R1D64

- sns.heatmap(data, annot=True, fmt=''): el fmt es el formato de las anotaciones, puede ser por ejemplo '.1f' para mostrar sólo un punto decimal (un punto flotante)
- df.corr(): Genera un DF de correlación útil para realizar el heatmap por ejemplo.
- Para enmascarar el triángulo superior derecho de un DF/heatmap: 
    - mask = np.zeros_like(corr) : Genera un array con la misma forma que el df 
    - mask[np.triu_indices_from(mask)] = True : Guarda sólo el triángulo superior derecho
    - sns.heatmap(... , mask=mask)
- Alternativa: mask = np.triu(corr), es más simple
- fig=nombrecatplot.fig: Para que acceda al Facetgrid de matplotlib el catplot. Deprecada, se usa figure ahora
- nombrecatplot.set_ylabels('nombre'): Cambiar el nombre del eje en un gráfico catplot


    