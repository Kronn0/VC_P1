# VC_P1
En este cuaderno hemos realizado las siguientes tareas:

**1. Crear una imagen de tamaño 800x800 con la textura de tablero de ajedrez.**

**2. Crear ua imagen estilo Mondrian (ejemplo https://www3.gobiernodecanarias.org/medusa/ecoescuela/sa/2017/04/17/descubriendo-a-mondrian/).**

**3. Resolver una de las tareas previas (elegida la tarea 1 ) con las fuciones de dibujo de OpenCV.**

**4. Modificar de alguna forma los valores de un plano de la imagen.**

**5. Pintar círculos en las posiciones del píxel más claro y oscuro de la imagen y hacerlo con las zonas más oscura y clara 8x8.**

**6. Una propuesta de pop Art.**


**1. Crear una imagen de tamaño 800x800 con la textura de tablero de ajedrez**

Para ello hemos de saber de cuanto es un tablero de ajedrez, para poder dividir el canvas y así dibujar los cuadrados
Segun Wikipedia (https://es.wikipedia.org/wiki/Tablero_de_damas_y_ajedrez) es un 8x8, bastante conveniente porque podemos hacer que los cuadrados sean de 100x100 y así poder dividir el tablero
primero debemos hacer un canvas de 800x800 y pintarlo de negro. luego dividimos el tablero en 8x8 y lo recorremos con un doble bucle.
Cuando encuentre una celda donde la suma de la fila y la de la columna den un numero par entonces rellenamos desde la esquina  de la fila anterior y la columa anterior hasta la esquina actual.

**2. Crear una imagen estilo Mondrian (ejemplo https://www3.gobiernodecanarias.org/medusa/ecoescuela/sa/2017/04/17/descubriendo-a-mondrian/)**

Para ello he pensado que podriamos utilizar elementos aleatorios para generar un Mondrian cada vez que se genere la imagen.

Primero creamos el canvas y lo rellenamos de blanco. definimos cuantos rectangulos quiero en mi Mondrian, hacemos un bucle el numero de veces que hayamos definido. Genero 4 puntos coordinales dentro del espacio de mi canvas, y luego genero un color generando 3 numeros entre 0 y 255. Cogiendo los 4 puntos selecciono donde pintar el rectangulo y luego con el color generado de que color lo genero, luego pinto de nuevo donde el anterior pero pinto un rectangulo con borde negro para que quede más como un Mondrian.

**3. Resolver una de las tareas previas (elegida la tarea 1 ) con las fuciones de dibujo de OpenCV**

Como la tarea 2 ya se hizo con OpenCV se decidio hacer la primera nuevamente. Para ello debemos de repetir el proceso de crear el canvas, pintarlo de negro y de recorrer el canvas dividiendolo en un 8x8. Cuando se cumpla que la suma de la fila y de la columna de par entonces usamos OpenCV para pintar un rectangulo con los puntos de la esquina de la fila y la columna anterior hasta la esquina de esta fila y columna.

**4. Modificar de alguna forma los valores de un plano de la imagen**

En esta tarea se ha hecho un cambio del espacio del color BGR -> HSV para poder jugar con la saturación de los colores y así poder aislarlos dentro de un rango que se ha definido. Luego se realiza una operacion AND a cada bit de cada color para así crear una máscara que luego se aplicará al frame y dará como resultado el aislamiento de cada color. Se presenta con tres ventanas, una normal de la cámara, otra con la máscara y la última con la máscara aplicada al frame para una sencilla comparación.

Fuente de la idea: https://docs.opencv.org/4.x/df/d9d/tutorial_py_colorspaces.html


**5. Pintar círculos en las posiciones del píxel más claro y oscuro de la imagen y hacerlo con las zonas más oscura y clara 8x8**

Para ello vamos a sub-dividir el problema en dos, en encontrar un solo pixel y el de encontrar la zona 8x8. 

Para el primer problema pues pasamos el frame de la camara a una escala de gris, para encontrar cual pixel es más oscuro o más claro. Luego usamos una fución de OpenCV llamada "minMaxLoc" Que localiza el valor máximo y minimo de un pixel en la imagen y donde se localiza en esa imagen. Luego con OpenCV pintamos donde haya localizado el pixel más oscuro un circulo negro de radio 3 y relleno, y lo mismo pero con un circulo blanco para el pixel más claro. 

Para el segundo problema debemos de recorrer la imagen de una manera más manual, primero debemos de pasar el frame a escala de gris nuevamente. sacamos las dimensiones del frame, definimos el tamaño de la zona que queremos encontrar, este caso 8 (8x8), declaramos la intensidad minima de la zona como infinity ya que cualquier pixel va a ser siempre más pequeño que esta y la intensidad maxima de la zona como -1 porque cualquier pixel va a ser mayor que ella. Luego definimos variables de coordenadas para el maximo y el minimo. 

recorremos la imagen desde 0 hasta el tamaño de esta menos 8 pixeles (+ 1 para que no haya Out of bounds) y la vamos saltand de 8 en 8. Creamos una matriz desde el pixel en el que estamos hasta 8 pixeles más, hacemos la media de esa region y tenemos la intensidad de la zona, si la intensidad es menor que el minimo actual entonces actualizamos el minimo y guardams las coordenadas del pixel, si es mayor que el maximo actual hacemos lo mismo. 

Una vez acabado el doble bucle. Pintamos el circulo negro donde las coordenadas de la intensidad maxima y el circulo blanco donde la maxima.

**6. Una propuesta de pop Art**

Basicamente hemos cogido el del ejemplo anterior y lo hemos retocado para que el frame nuevo en vez de ser solo blanco y negro pueda aceptar más colores y hemos cogido una paleta de colores de pop art y lo hemos implementado en este para que el fondo y los dots sean de diferentes colores. 

fuente de los colores: https://www.schemecolor.com/pop-art.php