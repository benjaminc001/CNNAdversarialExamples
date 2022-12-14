# Defensa adversaria en redes neuronales convolucionales
## EL4106 - Inteligencia Computacional

### Integrantes:
Benjamín Castro R. y Jordan Pérez D.

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
Abra el archivo en una terminal de **Google Colab**, aquí debe realizar el mismo procedimiento con la respectiva carpeta */data* y los pesos de la red **Le-net** que se mostraron en la generación con el método anterior. Además, debe cargar las etiquetas del *dataset* ImageNet (archivo *imagenet_class_index.json*) y la imagen *chihuahua2.jpg*. Luego de esto, puede correr el código presente en el *notebook* y visualizar la introducción y los resultados.
#### Implementación de ataque PGD
El código muestra un introducción al problema de ataques adversarios mediante PGD con la prueba en el modelo pre-entrenado usando la red **ResNet50** y el error en la clasificación de la imagen por parte de la red.

Luego de la introducción, carga el *dataset* MNIST, el modelo pre-entrenado **Le-Net** y sus respectivos pesos. Además, define en una función el método de ataque PGD con las variables de imagen $X$, la etiqueta $y$ con la que se desea confundir al modelo; el parámetro $\varepsilon$ que controla el intervalo entre el cual está acotada la perturbación, el paso de iteración $\alpha$ y el número de iteraciones. Retorna la perturbación y el valor de la pérdida luego de aplicar *backpropagation* en las iteraciones. 

Las función de evaluación del modelo corresponde a la de cálculo de *accuracy*, la cual compara las predicciones con datos perturbados con respecto a las etiquetas reales. Además, se muestra una visualización de los datos post-evaluación del modelo con ejemplos generados por la función y los gráficos de *accuracy* en función de $\varepsilon$.
### 3. Entrenamiento adversario (archivo *Adv_training.ipynb*)
Se presenta el *dataset* de CIFAR-10, el modelo pre-entrenado ResNet 18 y dos funciones de épocas, una normal, donde se introduce el *dataloader* correspondiente y el modelo, y otra adversaria, donde además se puede cargar el ataque (FGSM o PGD). Se corren las celdas correspondientes para poder ver el efecto que tiene el entrenamiento adversario en el desempeño del modelo. Se pueden ir cambiando los hiperparámetros de los ataques para medir su funcionamiento, además, se recomienda dejar constante el número de épocas de entrenamiento, debido a que esto optimiza el tiempo en el que se corre el archivo. Con esta cantidad se logra lo necesario que se quiere demostrar: el entrenamiento adversario supera al entrenamiento normal para los ejemplos adversarios.

**Es recomendable usar GPU para esta parte.**

### 4. Ataque a caja negra (archivo *BlackBoxAttack.ipynb*)
Abrir el archivo en una terminal de **Google Colab** y cargar los labels de ImageNet presentes en la carpeta de *Intro_and_PGD*. Cuando se tienen listos, se presenta un modelo de caja negra (se descarga en el mismo terminal) y se pueden ir cargando imágenes para poder observar las predicciones de este modelo y los *labels* con los que este clasifica. 

Por otro lado, se cargan modelos pre-entrenados ResNet 50 y VGG-16 (sustitutos), con los que también se pueden cargar imágenes para comparar las predicciones con respecto a la caja negra. Se deben correr las celdas de manera individual, donde está detallado por sección qué es lo que hace cada celda.
