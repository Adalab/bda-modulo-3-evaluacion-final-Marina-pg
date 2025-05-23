EDA VUELOS:
- 405624 filas.
- Todas las columnas son numéricas: todas int, Points Accumulated float.
- No existen valores nulos en ninguna columna.
- Columnas a eliminar: Dollar Cost Points Redeemed. Es una columna muy útil para la fidelización de clientes pero no en el objetivo del análisis, por lo que he decidido eliminarla para tener un DataFrame lo más sencillo posible de leer y analizar en función del objetivo.


EDA CLIENTES:
- 16737 filas.
- Todas las columnas tienen el formato correcto.
- Valores nulos: Salary (25%), Cancellation Year, Cancellation Month.
- Columnas a eliminar: Country, Cancellation Year, Cancellation Month, Enrollment Year, Enrollment Month. En el objetivo del análisis no aportan información relevante y así queda un DataFrame más sencillo de leer e interpretar.
- En la columna Salary hay valores negativos. Tras consultarlo con el departamento correspondiente me indican que ha sido una errata, por lo que los convertiré en positivos.


UNIÓN:
- Realizo la unión de los dos DataFrame con un merge on left, poniendo a la izquierda la información de todos los vuelos cogidos por los clientes y a la derecha la información del cliente asociado a cada vuelo, usando como columna de unión Loyalty Number.


LIMPIEZA DE DATOS:
- Compruebo si hay filas duplicadas y las elimino. 
- Elimino las columnas que he considerado durante el EDA. Queda un DataFrame con 403.760 filas y 19 columnas.
- Transformo los valores negativos en positivos en la columna Salary.
- Compruebo que ahora solo tengo valores nulos en la columna Salary, con un 25%. De entre todas las columnas, creo que podría haber relación con CLV (valor del cliente), Province o Education, pero tras comprobarlo veo que no existe una correlación entre las variables, por lo que no puedo aplicar IterativeImputer o KNNI para completar los valores nulos. Al tratarse de un cuarto de los valores nulos considero muy arriesgado completarlos con la mediana, que tiene bastante diferencia con la media, ya que esto podría afectar a la visualización de los datos y la correlación entre las variables dando resultados poco ajustados a la realidad, por lo que mantengo los nulos.


VISUALIZACIÓN:
- Comienzo a estudiar la relación que hay entre diferentes variables para dar respuesta al objetivo del análisis solicitado por el cliente. Estas conclusiones están en el archivo evaluacion_mod3 junto con la visualización de la relación entre las variables. Como next step lo pasaré a una presentación, de momento lo he dejado en el archivo para tener un apoyo visual junto con la conclusión extraída del análisis. A continuación detallo cómo he realizado este análisis:

- Distribución de vuelos por mes: primero es necesario realizar una agrupación de los vuelos por meses para sumar el total de vuelos reservados cada mes. A continuación veo la distribución de los vuelos reservados por mes con un Barplot.

- Relación entre la distancia recorrida en los vuelos y los puntos acumulados por el cliente: he utilizado un Regplot que me ayuda a ver de forma visual si existe una correlación lineal entre ambas variables.

- Distribución de los clientes por provincia: he sumado el número de Loyalty Number únicos que hay por provincia para ver gráficamente su distribución en un Barplot.

- Comparación del salario promedio en función del nivel de estudios: agrupo los datos por nivel educativo y calculo el salario promedio para cada nivel. Con el DataFrame extraído puedo ver que para College no hay datos, por lo que aunque lo dejo en el análisis para reflejar esto visualmente no podemos extraer ninguna conclusión sobre este nivel pero sí sobre los demás. Compruebo si los demás niveles educativos tienen algún valor nulo o se concentran todos en College. Le solicito a la empresa que me envíe los datos faltantes para poder realizar un análisis completo.

- Proporción de clientes con diferentes tipos de tarjetas de fidelidad: para conocer cuántos clientes hay por cada tipo de tarjeta agrupo los datos por tipo de tarjeta de fidelidad y cuento el número de Loyalty Numbers único para cada uno. Hago un Pieplot para conocer la proporción en porcentaje.

- Distribución por estado civil y género: utilizo un countplot para relacionar estas dos variables categóricas. En el eje y el número total de clientes y en el eje x el estado civil, añado un hue de género para poder visualizar los datos de forma más clara. También he hecho una tabla de contingencia como apoyo para la conclusión ya que muestra en forma de porcetaje la distribución de los datos de estado civil por género.


BONUS:
El cliente quiere conocer las estadísticas descriptivas (media, mediana, desviación estándar y varianza) de los vuelos reservados para cada grupo de nivel educativo.
Para ello primero he tenido que agrupar por 'Loyalty Number' y 'Education' y hacer una suma de los vuelos reservados, 'Flights Booked', para conocer el número total de vuelos reservados por cada cliente y su nivel educativo. Para a continuación agrupar por nivel educativo y calcular las estadísticas descriptivas de los vuelos reservados por cada grupo.