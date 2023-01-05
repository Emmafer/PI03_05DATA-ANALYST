# Análisis Exploratorio de Datos (EDA). 

En este informe encontraremos de forma narrada y resumida las decisiones tomadas a la hora de normalizar nuestros datos para luego analizarlos. Cabe destacar que todos los cambios realizados en las tablas fueron hechos con PowerQuery/DAX dentro del mismo archivo PowerBI en el que se encuentran las visualizaciones, además, todas estas decisiones fueron tomadas a partir de la decisión de encarar el proyecto como una comparación entre las ventajas que tiene invertir en instalar y promover servicios de Internet contra instalar servicios de Telefonía Fija en Argentina, basándonos en un rango de datos que va desde el 2014 al 2022.

## Selección de datasets:

Utilizaremos 6 tablas de las provistas por Enacom, 3 de ellas con datos sobre servicios de internet y otras 3 con datos sobre servicios de telefonía fija:

### - Internet  -

+ Penetración de Internet (Accesos por cada 100 hogares).

+ Acceso a Internet por tecnología y localidad.

+ Ingresos trimestrales por la prestación del servicio de Internet.

### - Telefonía Fija -

+ Penetración provincial de la telefonía fija (Accesos por cada 100 hogares).

+ Accesos de telefonía fija por provincia (hogares, comerciales, gobierno y otros).

+ Ingresos trimestrales por la prestación del servicio de telefonía fija.

## Importación de datasets a PowerBI y Normalización de las tablas:

Primero nos aseguramos de descargar todos los datasets en el mismo tipo de archivo (CSV) y subirlos en el mismo formato, separados por coma y con un encoding UTF-8.

Luego, creamos una tabla Calendario con distintas columnas con formato DATE que utilizaremos para vincular los datos y para facilitar la creación de medidas, además, todas nuestras tablas cuentan con columnas "Año" y "Trimestre", pero debido a que las mismas tienen un formato numérico que no nos sirve para realizar las medidas necesarias, creamos una columna "Fecha" utilizando el siguiente código en DAX: 

- `Fecha = DATE ( Tabla[Año], 1 + 3 * ( Tabla[Trimestre] - 1 ), 1 )`. 

Luego, para seguir con la normalización de datos, nos aseguramos de que todas las columnas "Provincia" de las distintas tablas tengan el mismo formato, ya que en algunos casos los valores se encuentran en mayúsculas o sin tildes. Esto último lo resolvemos de manera sencilla con PowerQuery, reemplazando los valores sin tilde como por ejemplo "Cordoba" -> "Córdoba". Para el problema de las mayúsculas utilizamos la función integrada de PowerBI que hace justamente lo que buscamos, mostrar las palabras con la primera letra mayúscula, por ejemplo "BUENOS AIRES -> Buenos Aires".

Necesitamos que nuestros datos esten normalizados para poder vincular las tablas entre sí, esto no solamente nos sirve para realizar las medidas con las que crearemos los KPI's, sino que nos sirve a la hora de visualizar nuestros datos, ya que si las tablas se encuentran vinculadas, al aplicar un filtro sobre un gráfico, se aplica el mismo filtro para todo el dashboard, haciendo que la presentación sea más dinámica y que los datos en los que nos apoyamos para acompañar nuestro story telling tengan una mejor calidad.

## Extras:

Hubieron pequeños cambios cuya única funcionalidad era facilitar y agilizar la lectura y creación de las medidas, como por ejemplo, renombrar las tablas o columnas, crear una carpeta separada de las tablas llamada "Medidas" donde incluímos todas las medidas creadas, etc.
