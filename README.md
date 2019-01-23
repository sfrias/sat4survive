# sat4survive
Localize indentify small boats on the sea

We're using sat public parametric data for radiance to identify possible small boats on movement or static

The goal is to democratize this info vs. private plattforms or not public data as FRONTEX, and other commercial.

![Frontex vs Sentinel-2 Comparison](https://github.com/sfrias/sat4survive/blob/master/doc_media/boat_detection.png)

To approach this fit, we're thinking about subpixel resolution propietary technologies and equivalent convolution network.
First problem is that resolution was 10 meters for pixel. Calculating final value for selected passed positions can variate on filter reached of 410 levels(6-7 humans) on 4x4 filter, around mean value of first filter (32x32), with values 0-255 for pixel. Can be possible.

Calculating filters for first, second, third and fourth convolution...Hard work was to make training and test dataset from official sources (this info becomes public and can be downloaded)



Salvar Vidas en el Mar con Tratamiento Datos Satélite

ANTECEDENTES:
http://www.publico.es/sociedad/migrantes-y-refugiados-muertos-mediterraneo-superan-3-000-cuarto-ano-consecutivo.html
Los migrantes y refugiados muertos en el Mediterráneo superan los 3.000 por cuarto año consecutivo.

OBJECTIVE:
The objective is to statistically locate small boats full of people sailing in a certain quadrant of the sea.

TECHNICAL ASSUMPTIONS:
For this, the first thing to do is make an appropriate choice of the data to be used (dataset quality).

 The goal, in this case, is to achieve the greatest success by maximizing certain positives or minimizing false negatives (criterion according to the valuation of the lives of people / resources invested in salvage), in a model that manages to differentiate that added direct radiation from small boats, when they are grouped or depart from an area at the time of sampling, with respect to areas of the sea where there is no such subtle anomaly in the radiation captured by some pixels.
 
The average infrared radiation of a human being at 37ºC is about 100W.

 Taking into account the pseudo-vertical position, crush, clothing, hair and head cover, a direct / interlaced minimum radiation of 6% is estimated, and scattered (inter-radiant or reflected in certain materials) of just another 4%, and that mix with possible reflections and coincident emissions dependent on the Sun (our main problem in false positives).
 
It could be received from a point in orbit said direct radiation, with a pessimistic average loss, dependent on climatic conditions ranging between 100% (water vapor clouds, typical absorption CO2, oxygen and other gases greenhouse effect) and 80% .

 This represents very small emission powers in a very small space:

- for tiny boats of 6-7 people in an area of ​​3x1 meters is a maximum of 130W in broad daylight. The estimated normalized value for a pixel of 10x10 meters is 3.9W and for a pixel of 20x20 meters it is only 1W.

- for small boats of 25-30 people in an area of ​​5x2 meters is a maximum of 540W in broad daylight. The estimated normalized value for a pixel of 10x10 meters is 54W, and for a pixel of 20x20 meters it is 13.5W

- for larger vessels, it is not evaluated as there are already reliable and mature detection methods and systems in place.

 But not all are setbacks, we also have information provided by other models:

The boats, when smaller, tend to sail in a group, perhaps because of a fundamental principle of mutual protection against shipwrecks.
The data provided by the satellites can be filtered fairly well from radiometric interference, also delimiting the cloud zones (highest proportion of water vapor drops) in each sampling.


Another point in favor of possible success of the model:
It is possible to work more with the infrared zones that show more significant differences before the dispersed increase of infrared radiation, with sensible differences between said bands.
 By Wien's Law of Law: For a black body, the product of the maximum radiation wavelength and the thermodynamic temperature is constant. As a result, when the temperature rises, the maximum radiant energy changes towards shorter wavelengths (higher energy and frequency) and towards the end of the spectrum.
When the maximum is evaluated from the Planck radiation formula, it is found that the product of the maximum wavelength and the temperature is constant. The preferred wave length is LambdaMax = 0.002898 / Temperature Kelvin.
In the mid-infrared, between 5um to 25um-40um, we have most of the thermal emission of the bodies at typical temperatures on the Earth's surface (several hundred Kelvin).

It has been proposed to use the facilities that can be provided by the Copernicus platform of the ESA, from the Sentinel Satellites fleet, which at least give us these samplings and resolutions by pantographic capture.


PRACTICAL EVALUATION OF THE ASSUMPTIONS:
We are going to carry out an exploratory analysis of a known area, where there are ships, with different resolutions resolutions of space per pixel and see the implications that it entails, before assembling the game of images for training and the game of test images, taking advantage of we have much more resolution images of the chosen places.



We have chosen the port of Tarragona for its activity with large and medium-sized boats, which is mixed with fishing fleets, and with small nautical recreation boats.



The first thing we are going to do is check if the length estimate per pixel is adjusted for a medium infrared channel, which will be the most used in detections.




The final breakwater of the port is measured having already the photo adjusted with the mask and the corresponding metadata. We see that it corresponds with the geographic information we have.





We are now going to estimate the dimensions of a ship that is perfectly visualized by the pixels and the shadow it projects in front of the sun. To the naked eye you can not see

# SPANISH

OBJETIVO:
El objetivo es localizar estadísticamente  pequeñas embarcaciones llenas de personas que navegan en un cuadrante determinado del mar. 

SUPUESTOS TECNICOS: 
Para ello lo primero que hay que hacer es hacer una elección adecuada de los datos a usar (calidad del dataset).

 La meta, en este caso es conseguir el mayor éxito al maximizar los positivos ciertos o minimizar los negativos falsos ( criterio según valoración de la vida de personas/recursos invertidos en el salvamento), en un modelo que consiga diferenciar esa radiación directa añadida procedente de pequeñas embarcaciones, cuando se agrupan o parten de un area en el instante que se hace el muestreo., respecto a areas del mar donde no aparece dicha sutil anomalía en la radiación captada por algunos píxeles.
 
La radiacion media infraroja de un ser humano a 37ºC viene a ser de unos 100W.

 Teniendo en cuenta la posicion pseudo-vertical, agolpamiento, vestimentas, pelo y cubrecabezas, se estima una radiación directa/ entrelazada mínima del 6%, y dispersa (inter-radiante o reflejada en ciertos materiales) de  apenas otro 4%, y que se mezcla con posibles reflexiones y emisiones coincidentes dependientes del Sol (nuestro principal problema en falsos positivos).
 
Se podrían recibir desde un punto en órbita dicha radiación directa, con una pérdida media pesimista, dependiente de las condiciones climáticas que oscila entre el 100% (vapor de agua nubes, absorción típica CO2, Oxígeno y otros gases efecto invernadero) y el 80%.

 Ello representa unas potencias de emisión muy pequeñas en un espacio muy reducido:

- para diminutas embarcaciones de 6-7 personas en un area de 3x1 metros es de un máximo de 130W en pleno día. El valor normalizado estimado  para un pixel de 10x10 metros es 3,9W y para un pixel de 20x20 metros es  de apenas 1W.

- para pequeñas embarcaciones de 25-30 personas en un area de 5x2 metros es de un máximo de 540W en pleno día. El valor normalizado estimado para un pixel de 10x10 metros es 54W, y para un pixel de 20x20 metros es 13,5W

- para mayores embarcaciones no se evalúa pues existen métodos y sistemas de detección ya fiables y maduros implantados.

 Pero no todo son contrariedades, también tenemos información que nos proporcionan otros modelos:

Las embarcaciones, cuando mas pequeñas, mas tienden a navegar en grupo, quizás por un principio fundamental de protección mútua ante naufragios.
Los datos proporcionados por los satélites se pueden filtrar bastante bien de interferencias radiométricas, delimitando también las zonas de nubes (mayor proporción de micro gotas de vapor de agua) en cada muestreo.



Otro punto a favor de posible éxito del modelo:
Se puede trabajar mas con las zonas de infrarojo que manifiesten diferencias más significativas ante el aumento disperso de radiación infraroja, con diferencias sensibles entre dichas bandas.
 Por la ley de Ley de Wien: Para un cuerpo negro, el producto de la longitud de onda de máxima radiación y de la temperatura termodinámico es constante. Como resultado, cuando la temperatura sube, la máxima energía radiante cambia hacia longitudes de ondas más cortas ( energía y frecuencia más alta) y hacia el final del espectro.
Cuando se evalúa el máximo a partir de la fórmula de radiación de Planck, se encuentra que el producto de la longitud de onda máxima y la temperatura es constante. La Longittud de onda preferente es LambdaMax = 0.002898/TemperaturaKelvin.
En el infrarrojo medio, entre 5um hasta 25um-40um, tenemos la mayor parte de la emisión térmica de los cuerpos a las temperaturas típicas en la superficie terrestre (varios cientos de kelvin).

Se ha planteado utilizar las facilidades que pueden ser cedidas por la plataforma Copernicus de la ESA, procedente de la flota de Satélites Sentinel, que como mínimo nos dan estos muestreos y resoluciones por captura pantográfica.








EVALUACION PRACTICA DE LOS SUPUESTOS:
Vamos a realizar un análisis exploratorio de un área conocida, donde haya barcos, con distintas resoluciones resoluciones de espacio por pixel y ver las implicaciones que conlleva, antes de montar el juego de imágenes para el entrenamiento y el juego de imágenes de prueba, aprovechando que tenemos imágenes de mucha mas resolución de los lugares elegidos.



Hemos elegido el puerto de Tarragona por su actividad  con grandes y medianos barcos, que se mezcla con las flotas de pesca, y con pequeñas embarcaciones de recreo náutico.



La primera cosa que vamos a hacer es comprobar si la estimación de longitud por pixel se ajusta para un canal de Infrarojo medio, que será el que mas utilizaremos en las detecciones.




Se mide la escollera final del puerto teniendo ya la foto ajustada con la máscara y los metadatos correspondientes. Vemos que corresponde bastante con la información geográfica de la que disponemos.





Vamos ya a estimar las dimensiones de un barco que se visualiza perfectamente por los  pixeles y la sombra que proyecta frente al sol. A simple vista no se ven elementos que puedan determinar movimiento. El barco aparece en la parte superior derecha, cerca de la esquina superior derecha de la aplicación de medida, y los extremos de la medida ligeramente en rojo. Se estima una longitud de unos 40 metros de eslora. El número de pixeles horizontales oscila entre dos y tres.


Se realiza otra comprobacion en esa direccion de medida, en este caso en una posicion mas alejada, al final del rompeolas.

Viene a dar una medida similar en metros, entrando la variacion en la tolerancia.

Ahora vamos a confrontar esa medida con la información geográfica de la que disponemos. Vemos que también coincide en gran medida. En el resto de dimensiones también se ve coincidencia a simple vista.

Por la otra parte de la foto también hay una similitud aceptable. La distorsión en la imagen y su precisión está bien corregida a priori.







Hay que recordar que siempre trabajamos con el mismo muestreo temporal, la misma variedad radiométrica, y el mismo canal. Trabajaremos en general con fotos radiométricas con resolucion espacial de un pixel cada 20 metros cuadrados, preferentemente en infrarojo medio, bandas 10 y 11





Para la creación diferentes imágenes de validación, nos valdremos de muestras radiométricas idénticas, pero de más resolución, con las que estableceremos el criterio de validación de forma fiable.

Aquí confrontamos la misma imagen, pero la de abajo, es de mayor resolución, concretamente de un pixel cada 10 metros cuadrados, y de un espectro visible, para poder evaluar de forma natural si ciertas entidades son barcos o no.


Parece una buena forma de determinar barcos parados y en movimiento, y nos hace fijar la atención en características que tienen unos y otros, cómo puede ser el rastro que deja una embarcación cuando se desplaza, cómo la que ahora se ve cerca de la punta del final de la escollera, de las sombras que generan los barcos mas grandes, y que no la generan los pequeños, de barcos adosados a muelles, del patrón de las olas, o del fondo de zonas poco profundas.


Perspectiva de recursos en el proceso de los datos
Retículas de 100Km con una resolucion de típica de 20 metros representan 5000 x 5000 pixeles; un total 25 millones de puntos por retícula que aparte de otros metadatos asociados a grupos, guardan un valor de medida en un rango de al menos 4096 valores, lo que representa un proceso de 300 millones de bits por retícula.
 Si la retícula tiene una resolución de 10 metros, representan 10.000 x 10.000 pixeles; un total de 100 millones de puntos, dando la friolera de 1200 millones de puntos por retícula de secciones con 100 kilómetros cuadrados.

 La idea de que un modelo pueda tener un grado alto de éxito es el concepto de resolución subpixel(la intensidad de un píxel representa un promedio de la señal recibida desde todo el recuadro), tendremos que procesar varias bandas, que se capturan con una diferencia de aproximadamente medio segundo. Un objeto en movimiento aparecerá desplazado en el mapa de pixeles y posiblemente con un rastro, en función de su velocidad, y uno quieto, debería generar un balance nulo en los promedios circundantes.



 El siguiente punto es evaluar en que medida es viable abarcar una zona determinada donde se realizarán las predicciones en cada ciclo de revisita satelital, y la repercusión en cuanto a recursos y efectividad. Cómo ejemplo se ha puesto la costa de Libia, desde donde parten numerosas embarcaciones de muy pequeño tamaño, totalmente saturadas de personas, que quieren alcanzar el otro lado del mediterraneo.

Otro tema importante será el de establecer máscaras en cada retícula de coordenadas para no tratar las areas que no se deben tratar: áreas de fotos que no están dentro de un área de navegación posible.

Ahora hay que estimar la cantidad de pixeles que se deberán procesar cada vez que haya una revisita del satélite. Tendremos una máscara por canal tratado, que inicialmente tendrá marcada el área de “cerca de tierra firme”, para que no se procesen esos píxeles de las fotos, y que a medida que se vayan procesando los grupos de píxeles con las distintas fotos aportadas se irán marcando para que no se vuelvan a tratar.


