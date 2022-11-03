![HenryLogo](https://d31uz8lwfmyn8g.cloudfront.net/Assets/logo-henry-white-lg.png)
​
# Proyecto individual 2
​
​
## Mercado inmobiliario
​
Dentro de la sociedad globalizada e industrializada, es sabido que los precios de los inmuebles han presentado un constante cambio, por lo que quienes deseen invertir o vender una propiedad se enfrentan al fenómeno especulativo existente en la valorización de éstos. Esto, debido a la constante tendencia de las ciudades a crecer demográfica y comercialmente, llegando a un punto en donde no se tiene certeza de la valorización real dentro del sector en donde se desee invertir. 
​
Pese a que el precio depende, en cierta medida, de las tendencias que esté teniendo el mercado inmobiliario en un determinado tiempo, poder estimar adecuadamente el valor de una propiedad es una referencia clave para entender si es una buena oportunidad, ya sea de compra o de venta.
​
## Descripción del problema
​
El proyecto se basa en pronosticar debido a diferentes característas del inmueble si se considera barato o caro. Algunas de la features a tener en cuenta es la cantidad de habitaciones, localización, descripción, superficie. Para solucionar este problema se analizan 2 .csv, uno que contine el precio de los inmbuebles, con lo cual se va a sacar la media general y a partir de ella dividir las propiedades en caras o baratas. Y el otro, que es el que tenemos que predecir la clasificación pero sin la lista de precios.
​
## Pasos seguidos
​
- Se abrieron los archivos y se convirtieron en los datos del csv en DataFrame con la ayuda de la librería pandas
- Se realizó la columna target
- Se hizo un análisis exploratorio de los datos como es ver la cantidad de datos nulos en cada columna, su correlación con la columna objetivo, limpieza de datos, etc
- Se borraron columnas que tenían muy pocos valores
- Se imputaron valores faltantes a las columnas que le faltaban datos y no se borraron.
- Se convirtieron a dummies las features categóricas.
- Se dejaron las features que tienen correlación mayor a 0.1 y menor -0.1
- Con este EDA realizado se procedió a probar sin éxito varios modelos con la librería Sklearn: vecinos más cercanos, árbol de decisión, regresión logística y random forest classifier
- Se probó modificando el EDA y convertir todas las features categóricas que contenían una buena cantidad de datos y en variables dummies. Se aplicó pca para reducir la dimensionalidad y se probó con random forest, que dió una valores mediocres.
- Volviendo otra vez sobre nuestros pasos, se decidió probar en vez de usar get_dummies de pandas, label enconder de sklearn para las features categóricas. No hubo buenos resultados. 
- Llegado este momento se cambió el análisis del EDA. Se decidió trabajar con las columnas que tuvieran una correlación aceptable aunque estuvieran mayormente vacías. A estas se les aplicó una imputación de valores por su mediana subdivida según el tipo de propiedad que eran y si el target las marcaba como baratas o nulas.
- Una vez llenas, se les aplicó get_dummies a las columnas categóricas.
- Se procedió a hacer el modelo y resultó en que las métricas que evalúan el rendimiento daban muy bien. Esto puede significar dos cosas, en que se obtuvo un buen modelo o que se overfitteo el modelo y no se va a adaptar bien a los nuevos datos.
- Para sacarse las dudas se uso el csv de testeo, al cual se les aplicó los cambios correspondientes, y se llegó a la conclusión de que efectivamente, el modelo está overfitteado. Se llegó como mejor puntaje a un recall de    0.55 y un accuracy de 0.72.
- Con las últimas horas en marcha, se decidió cambiar la forma de imputación de valores en el dataframe Test pero no hubo buenos resultados, mejoró unos puntos el recall a consecuencia de bajar drásticamente el accuracy.
- Se llegó a la conclusión de que el problema es la base, es decir el EDA, por lo que todavía queda mucho por aprender y aplicar en este proyecto, como por ejemplo procesamiento de lenguaje natural. 
​
## Métrica utilizadas
​
Como método de evaluación del desempeño del modelo, se utilizó la métrica de Exhaustividad (Recall) para las propiedades caras, a partir de la matriz de confusión (Confusion Matrix). 

Adicionalmente, se incluye la Accuracy como métrica de control.
​
## Archivos utilizados
​
Se utilizaron los archivos dentro del archivo comprimido 'properties_colombia.zip':
 - 'properties_colombia_train.csv': Contiene 197549 registros y 26 dimensiones, el cual incluye la información **numérica** del precio.
 - 'propiedades_colombia_test.csv': Contiene 65850 registros y 25 dimensiones, el cual no incluye la información del precio. 
​
## Descripción de las dimensiones
- id - Identificador del aviso. No es único: si el aviso es actualizado por la inmobiliaria (nueva versión del aviso) se crea un nuevo registro con la misma id pero distintas fechas: de alta y de baja.
- ad_type - Tipo de aviso (Propiedad, Desarrollo/Proyecto).
- start_date - Fecha de alta del aviso.
- end_date - Fecha de baja del aviso.
- created_on - Fecha de alta de la primera versión del aviso.
- lat - Latitud.
- lon - Longitud.
- l1 - Nivel administrativo 1: país.
- l2 - Nivel administrativo 2: usualmente provincia.
- l3 - Nivel administrativo 3: usualmente ciudad.
- l4 - Nivel administrativo 4: usualmente barrio.
- l5 - Nivel administrativo 5.
- l6 - Nivel administrativo 6.
- rooms - Cantidad de ambientes.
- bedrooms - Cantidad de dormitorios (útil en el resto de los países).
- bathrooms - Cantidad de baños.
- surface_total - Superficie total en m².
- surface_covered - Superficie cubierta en m².
- price - Precio publicado en el anuncio.
- currency - Moneda del precio publicado.
- price_period - Periodo del precio (Diario, Semanal, Mensual)
- title - Título del anuncio.
- description - Descripción del anuncio.
- property_type - Tipo de propiedad (Casa, Departamento, PH).
- operation_type - Tipo de operación (Venta).
- geometry - Puntos geométricos formados por las coordenadas latitud y longitud. 
​
## Aclaración

La carpeta resultados, es la carpeta en la cual aparecen las distintas predicciones que se han obtuvieron con los diferentes modelos con el dataset de test. Los nombres están ordenados según como de manera ascendente, es decir el primer archivo cargado es "Sebas1412.csv" y el último "Sebas1412(6).csv", tal como aparece en el dashboard.