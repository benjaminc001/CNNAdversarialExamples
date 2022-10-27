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
En primer lugar, abra el archivo en una terminal de **Google Colab**, donde debe crear una carpeta llamada */data* en la raíz principal (*content*). Aquí, suba el archivo *lenet_mnist_model.pth*, donde estarán los pesos de la red neuronal (arquitectura **Le-Net**) pre-entrenada. Luego, puede correr con normalidad cada celda del código para la observación de los resultados.

#### Implementación de ataque FGSM:
El código tiene tres componentes principales: una que corresponde a la carga y normalización del *dataset* MNIST, otra que es la función que genera las imágenes perturbadas mediante ataque FGSM (en función de una imagen, un gradiente y un valor $\varepsilon$) y la última que corresponde a la función para probar el comportamiento del modelo pre-entrenado en modo de evaluación con respecto a los datos (función *test*).

Los datos se cargan con un *loader*, el cual sirve como un iterable para la función *test*. Esta última utiliza una función de pérdida que permite dimensionar el ajuste de las predicciones realizadas con los datos perturbados con respecto a las predicciones originales del modelo pre-entrenado, realizando *backpropagation* para determinar los valores de pérdida que son almacenados para luego graficar en función de un $\varepsilon$ dado, al igual que el *accuracy* el cual es medido al comparar los aciertos de la red en función de las predicciones originales. Las imágenes correspondientes son guardadas en la raíz principal de la terminal.

### 2. Generación de ejemplos con método PGD (archivo *Introducción_y_PGD.ipynb*)
Abra el archivo en una terminal de **Google Colab**, aquí debe realizar el mismo procedimiento con la respectiva carpeta */data* y los pesos de la red **Le-net** que se mostraron en la generación con el método anterior. Además, debe cargar las etiquetas del *dataset* ImageNet (archivo *imagenet_class_index.json*) y la imagen *pig.jpg*. Luego de esto, puede correr el código presente en el *notebook* y visualizar la introducción y los resultados.
#### Implementación de ataque PGD
El código muestra un introducción al problema de ataques adversarios mediante PGD con la prueba en el modelo pre-entrenado usando la red **ResNet50** y el error en la clasificación de la imagen por parte de la red.

Luego de la introducción, carga el *dataset* MNIST, el modelo pre-entrenado **Le-Net** y sus respectivos pesos. Además, define en una función el método de ataque PGD con las variables de imagen $X$, la etiqueta $y$ con la que se desea confundir al modelo; el parámetro $\varepsilon$ que controla el intervalo entre el cual está acotada la perturbación, el paso de iteración $\alpha$ y el número de iteraciones. Retorna la perturbación y el valor de la pérdida luego de aplicar *backpropagation* en las iteraciones. 

Las función de evaluación del modelo corresponde a la de cálculo de *accuracy*, la cual compara las predicciones con datos perturbados con respecto a las etiquetas reales. Además, se muestra una visualización de los datos post-evaluación del modelo.

Las funciones que se utilizan para evaluar el modelo con 
