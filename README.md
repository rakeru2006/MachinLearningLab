# MachinLearningLab

buscar en google colaborative 

https://research.google.com/colaboratory/

[![Watch the video](https://i.imgur.com/vKb2F1B.png)](https://www.youtube.com/watch?v=inN8seMm7UI)





## Usar un dataset externo
Vamos a utilizar un dataset con información sobre películas. El enlace de éste dataset está aquí:

## Importamos librerías

```
import pandas as pd
import numpy as np
from sklearn.linear_model import LinearRegression
```


## Leemos el dataset
```
peliculas = pd.read_csv("movies2.csv")
```


Si abres el archivo movies2.csv verás que contiene distintos valores. Para realizar la regresión lineal solo necesitamos los valores numéricos.

## Seleccionar solo los valores numéricos

```
datos_numericos = peliculas.select_dtypes(np.number)
```

Aunque ya seleccionamos solo los valores numéricos, algunos de éstos contienen valores NaN (No es un número), por lo que vamos a reemplazarlos por 0.

```
datos_numericos = peliculas.select_dtypes(np.number).fillna(0)
```

## Configurar las variables objetivo e independientes.

En nuestro caso deseamos predecir a cuánto ascenderá el monto de ventas de cierta película. Por lo que estableceremos eso como nuestra variable objetivo. Las variables independientes serán todas las demás variables numéricas que no son el objetivo.

```
objetivo = "ventas"
#las variables independientes serian todas las demas menos ventas
independientes = datos_numericos.drop(columns=objetivo).columns
```

## Creamos el modelo y lo ajustamos
```
modelo = LinearRegression()
modelo.fit(X=datos_numericos[independientes], y=datos_numericos[objetivo])
```

## Agregamos las predicciones como una nueva columna del dataset original
```
peliculas["ventas_prediccion"] = modelo.predict(datos_numericos[independientes])
```

En la línea anterior, al dataset original (“peliculas”), le agregamos una nueva columna (“ventas_prediccion”) que contendrá el resultado de la predicción pasando todos los datos de las variables independientes.

Mostrar solo los campos ventas y ventas_predicción
```
print (peliculas[["ventas", "ventas_prediccion"]].head())
```

En la línea anterior imprimimos las columnas ventas y ventas_predicción, solo los primeros 5 resultados.

Resultados
