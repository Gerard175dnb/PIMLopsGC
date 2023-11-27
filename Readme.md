<p align=center><img src=https://d31uz8lwfmyn8g.cloudfront.net/Assets/logo-henry-white-lg.png><p>

# <h1 align=center> **PROYECTO INDIVIDUAL Nº1** </h1>

# <h1 align=center>**`Exploratory Data Analysis`**</h1>

El siguiente análisis tiene como objetivo mostrar gráficamente los pasos realizados y detallados en el ETL y el EDA, por favor, para mas detalles ingresar a los archivos mencionados



# Output_steam_games

Al abrir nuestro archivo *output_steam_games*, observamos que la cantidad de nulos representa más del 70% de nuestros datos totales, con lo cual procedimos a eliminar con (how='all') solo los nulos que en sus filas abarcan el total de columnas.


**Cantidad de nulos por columna**
publisher :      96362,
genres:          91593,
app_name:        88312,
title:           90360,
url:             88310,
release_date:    90377,
tags:            88473,
reviews_url:     88312,
specs:           88980,
price:           89687,
early_access:    88310,
id:              88312,
developer:       91609

![Descripción de la imagen](./Graficos/output.png)


Después de realizar ésta eliminación de nulos, renombramos las diferentes columnas que posee nuestro dataset df_steam_games para poder tenerlo más ordenado y verficamos de vuelta nuestra *cantidad de nulos*: 

publisher       8051,
genres          3282,
item_name          1,
title           2049,
url                0,
release_date    2066,
tags             162,
reviews_url        0,
specs            669,
price           1377,
early_access       0,
item_id            0,
developer       3298

![Descripción de la imagen](./Graficos/games.png)

Luego de revisar nulos y duplicados, encontramos datos faltantes en genres, pero encontramos similitud con la columna tags, la cual poseía géneros del juego observado, procedemos a realizar una funcion que tome como indice los valores unicos en géneros, para iterar por fila en tags y rellenar los valores faltantes en genres, luego procedimos a eliminar tags y eliminar datos en genres como "early_acces" o "free to play" ya que no son considerados generos


![Descripción de la imagen](./Graficos/genres.png)

# Australian User reviews


*Columnas al abrir nuestro archivo*
***user_id,	user_url,	reviews***

éstas son las columnas que nos quedan una vez desanidado reviews, procedemos a eliminar la columna "0", "helpful", "last_edited" y "funny" que son irrelevantes para nuestro análisis, encontrandonos con mucha felicidad que no poseemos nulos en esta instancia 

## ***user_id	,user_url	,funny	,posted	,last_edited	,item_id	,helpful	,recommend	,review,	0***
Luego, rellenamos la columna "year" con la media para poder sacar los valores faltantes, ésta columna es relevante para nuestro analisis y modelado futuro de datos, por lo tanto utilizamos .median en year

Podemos observar con wordcloud, las palabras más utilizadas en nuestra columna review, para poder observar de manera indirecta la futura anileación de sentimientos 


![Descripción de la imagen](./Graficos/cloud.png)

Tambien observamos la columna recommend para comparar

![Descripción de la imagen](./Graficos/Recommend.png)

# Sentiment Analysis 

Para nuestro análisis de sentimiento, utilizamos la libreria NLTK, la cual, con sentiment_vader, explora las reviews analizando el texto y devuelve valores como 0,1,2, en los cuales 2 es positivo, 1 es neutral(el cual tambien puede ser contemplado para usuarios que no dejaron reseña) y 0 para negativo, añadiendo la columna "sentiment_analysis" para nuestro dataset

![Descripción de la imagen](./Graficos/sentiment.png)
Acá podemos observar la cantidad de sentimientos en el total de reviews, siendo más positivos que negativos y neutros

***sentiment_analysis***
***2 :   33524,***
***1  :  13062,***
***0   : 12747***

Seguido a lo realizado, procedemos a eliminar duplicados y nulos, que para nuestra grata sorpresa eran bastante pocos y pudimos continuar al siguiente dataset, obteniendo user_reviews de esta manera:
## 'user_id',	'user_url',	'item_id'	,'recommend',	'year',	'sentiment_analysis'


# ***Australian user items***