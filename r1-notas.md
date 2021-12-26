**Comienzo este archivo en el día 44. Me pareció una buena forma de rastrear el proceso, tomar notas y poder encontrarlas después**

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

