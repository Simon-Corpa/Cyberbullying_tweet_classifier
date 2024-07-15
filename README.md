# Cyberbullying_tweet_classifier
Formulación de un modelo de clasificación de tweets en base a muestra de tweets con presencia de cyberbullying entrenado mediante el repositorio de Kaggle "[Cyberbullying Classification](https://www.kaggle.com/datasets/andrewmvd/cyberbullying-classification/data)", creado por Larxel.

El proyecto forma parte de la actividad evaluatoria del módulo Text Mining y redes sociales del Máster Data Science, Big Data & Business Analytics de la Universidad Complutense de Madrid, impartido por Luis Gascó.

## Metodología
El proyecto se divide en dos cuadernos de Jupiter redactados y ejecutados mediante Google Colab. Ambos pasan por los mismos procesos, iniciandose con un análisis preexploratorio y terminando con el entrenamiento y la validación de un modelo.

El primer cuaderno [Metodo1 main.ipynb](https://github.com/Simon-Corpa/Cyberbullying_tweet_classifier/blob/main/Metodo1%20main.ipynb) basa los modelos en la propia muestra obteniendo predicciones con un mayor error. El segundo cuaderno [Metodo2 main.ipynb](https://github.com/Simon-Corpa/Cyberbullying_tweet_classifier/blob/main/Metodo2%20main.ipynb), aprovecha la inclusión de modelos preentrenados de Huggingface mediante la libreria Transformers con el objetivo de simplificar las tareas de tokenización y modelización.

### Análisis exploratorio, pre-procesado y normalización de los datos 
Obtenemos el corpus y realizamos los imports.

#### En [Metodo1 main.ipynb](https://github.com/Simon-Corpa/Cyberbullying_tweet_classifier/blob/main/Metodo1%20main.ipynb):
Eliminamos duplicados, comporabmos el balance de la muestra, analizamos la distribución de una variable que contenga el número de caracteres de cada tweet y generamos Wordclouds entorno a las muestras con y sin cyberbullying.

Normalizamos el texto mediante supresión de espacios y conversión a minúsculas. Sustitución de contracciones, conteo de los cambios y análisis de su distribución. Tokenizamos y normalizamos urls, menciones y números. Suprimimos stopwords. Contamos presencia de hastags.

#### En [Metodo2 main.ipynb](https://github.com/Simon-Corpa/Cyberbullying_tweet_classifier/blob/main/Metodo2%20main.ipynb):
Obviamos el análisis exploratorio contenido en el cuaderno previo y llevamos a cabo el preprocesado y normalización mediante el modelo _bert-base-uncased_ y la función AutoTokenizer.

### Vectorización de textos 
#### En [Metodo1 main.ipynb](https://github.com/Simon-Corpa/Cyberbullying_tweet_classifier/blob/main/Metodo1%20main.ipynb):
Vectorización TfIdf mediante _TfidfVectorizer_.
#### En [Metodo2 main.ipynb](https://github.com/Simon-Corpa/Cyberbullying_tweet_classifier/blob/main/Metodo2%20main.ipynb):
Obtenemos una función para trabajar con el estratificador de muestras de testeo de sklearn aplicando el Trainer de la libreria _Transform_ mediante el uso de una clase cedida en las instrucciones del proyecto planteado por Luis Gascó.

### Entrenamiento y validación del sistema
Generamos muestras de entrenamiento y testeo y una función de validación cruzada para la evaluación de modelos de Regresión Logística, Naive Bayes Gaussiano y Arbol de Aleatoriedad. Aquel con mejores resultados pasa a tener una reevaluación mediante el establecimiento de nuevos hiperparametros.

Predecimos la variable dependiente en la muestra de testeo y hacemos un análisis de la importancia de las características del modelo.

# Resultados y conclusiones
La presencia de falta de concordancia a la hora de etiquetar la variable dependiente entre los responsables de hacerlo nos impide llegar a una predicción total. Un análisis exploratorio que examinase la proporción en la que tweets duplicados tienen valores contrarios entorno a su clasificación con respecto al total nos mostraría el error de muestreo que ya estaría absorbiendo el modelo, si bien el error podría aumentar en predicciones de muestras alternativas si este existe tambien en elementos no duplicados.

Al margen de los bloques de texto que llevan consigo conclusiones y explicaciones a lo largo de los dos cuadernos cabe destacar la mejora de eficacia de la segunda metodología si bien una comprensión desgranada de cada apartado llevada a cabo en el primer archivo permite ser consciente del grado de complejidad y los pasos y herramientas que se plantean durante estos procesos.
