# Defensa adversaria en redes neuronales convolucionales
## EL4106 - Inteligencia Computacional

### Integrantes:
Benjamín Castro R.\\
Jordan Pérez D.

### Ayudante:
Andrés González

### Profesor:
Pablo Estévez

### Auxiliar:
Juan Urrutia

## Instrucciones de ejecución:
### 1. Generación de ejemplos con método FGSM (archivo *FGSM_ex_generation.ipynb*)
En primer lugar, abra el archivo en una terminal de **Google Colab**, donde debe crear una carpeta llamada /data en la raíz principal (content). Aquí, suba el archivo *lenet_mnist_model.pth*, donde estarán los pesos de la red neuronal (arquitectura **Le-Net**) pre-entrenada. Luego, puede correr con normalidad cada celda del código para la observación de los resultados.

#### Implementación de ataque FGSM:
El código tiene tres componentes principales: una que corresponde a la carga y normalización del *dataset* MNIST, otra que es la función que genera las imágenes perturbadas mediante ataque FGSM (en función de una imagen, un gradiente y un valor $\varepsilon$) y la última que corresponde a la función para probar el comportamiento del modelo pre-entrenado en modo de evaluación con respecto a los datos (función *test*).

Los datos se cargan con un *loader*, el cual sirve como un iterable para la función *test*. Esta última utiliza una función de pérdida que permite dimensionar el ajuste de las predicciones realizadas con los datos perturbados con respecto a las predicciones originales del modelo pre-entrenado, realizando *backpropagation* para determinar los valores de pérdida que son almacenados para luego graficar en función de un $\varepsilon$ dado, al igual que el *accuracy* el cual es medido al comparar los aciertos de la red en función de las predicciones originales. 

### 2. Generación de ejemplos con método PGD (archivo )

####
