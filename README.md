# <center> **Porcesamiento y mejora de astrofotografía planetaria empleando Generative Adversarial Networks** </center>

<center>

</center>

*   Arantxa Camil Junco Flores  
*   Diego Antonio Villalba González
*   Jonathan Alexis Hernández Cuevas


<center> 

## **Resumen**
 </center>
En este proyecto exponemos el proceso de desarrollo de una Generative Adversarial Network junto al procesamiento de imágenes planetarias con el fin de mejorar la resolución, detalle y contraste de las imágenes obtenidas de fuentes de baja resolución y alto ruido intrínseco o fuentes externas.

Obtuvimos resultados satisfactorios aplicables a diferentes áreas de procesamiento de imágenes en la industria, como cámaras de seguridad, ultrasonidos, etc.

<img src="/results/moon_result.jpeg" title="Resultados en la luna">

<div id='id1' />  

## **Introducción**

<ul>
    <li>1.1 La astrofotografía </li>
La astrofotografía combina la astrofísica y la fotografía para capturar imágenes del cielo nocturno y objetos astronómicos. Ha experimentado una evolución desde las placas fotográficas hasta las cámaras digitales de alta resolución.

![Astro_1](https://www.rmg.co.uk/sites/default/files/styles/full_width_1440/public/PS2195402171243_Highly%20Commended_Cosmic%20Plughole%20%C2%A9%20James%20Stone_0.jpg?itok=yiNJeW76)


Los avances tecnológicos han permitido tiempos de exposición más cortos y la visualización instantánea de imágenes, mejorando los resultados. También se han desarrollado equipos especializados, como telescopios motorizados y sistemas de seguimiento.

Sin embargo, la astrofotografía enfrenta desafíos como la contaminación lumínica, que reduce la calidad de las imágenes y requiere viajar a áreas con cielos oscuros. El ruido electrónico de las cámaras digitales y la estabilidad del seguimiento del telescopio también son problemas a superar.

![Astro_2](https://cdn.eso.org/images/screen/dark-skies.jpg)

![Astro_3](https://www.cloudynights.com/uploads/monthly_01_2006/post-14351-14070956155523.jpg)


<li>1.2 Las SRGAN </li>
El SRGAN utiliza una arquitectura basada en Generative Adversarial Networks (GANS), que consiste en dos redes neuronales en competencia: el generador y el discriminador. El generador es responsable de tomar una imagen de baja resolución como entrada y generar una versión de alta resolución de la misma. El discriminador, por otro lado, tiene la tarea de distinguir entre las imágenes generadas por el generador y las imágenes reales de alta resolución.

![Astro_4](https://production-media.paperswithcode.com/methods/Screen_Shot_2020-07-19_at_11.13.45_AM_zsF2pa7.png)


La idea principal detrás de SRGAN es que el generador aprenda a generar imágenes de alta resolución que sean difíciles de distinguir de las imágenes reales de alta resolución, mientras que el discriminador aprende a identificar las imágenes generadas y las imágenes reales. A medida que estas dos redes compiten entre sí, se produce un proceso de aprendizaje en el que el generador mejora continuamente su capacidad para generar imágenes más realistas y de alta calidad.


<li>1.3 Porblemática a desarrollar</li>

Dentro de la astrofotografía el area de la astrofotografía planetaria es una de las más retadoras, recordemos que los planetas son objetos muy pequeños dentro del cielo nocturno además de que recorren el cielo nocturno con gran velocidad, aunado a las diferentes fuentes de interferencia natural y artificial hacen que el tomar una unica fotografía entrege reultados de baja calidad, es así que uno de los procesos mas comunes para disminuir el ruido ambiental y la aberración cromatica generada por el rápido movimiento de los planetas es la toma de un video con un camara colocada en el telescopio, grabando de manera continua el objeto en un intervalo de tiempo.

[Ejemplo de video de luna empleado en este notebook](https://drive.google.com/file/d/1zZpBY8-_lqFtdxu65OUoj4IY653Ls3Ly/view?usp=share_link)

[Ejemplo de video de Jupiter empleado en este notebook](https://drive.google.com/file/d/1WKNzMGnaJxTFWAIEgbwu-bm1BF1oW22x/view?usp=share_link)


Posteriormente se extraen los mejores frames de el video por medio de diferentes programas, los cuales promedian la información de cada frame y entregan una imagen, la cual puede ser procesada posteriomente en un proggrama de edición fotográfica.

![Astro_1](https://skyandtelescope.org/wp-content/uploads/Figure-4-web.jpg)


Sin embargo la calidad del resultado presenta importantes limitaciones, al emplear un video para obtener la información estamos limitados a la resolcuón del mismo para la fotografía final, teniendo como ejemplo fotografias de 1920 x 1080 pixeles en caso de que el video haya sido tomado en calidad full hd.

![Superficie lunar resultante de un video full hd](https://m.media-amazon.com/images/I/61etx+8gdCL._CR289,0,1154,1154_UX256.jpg)

Es por esto que buscamos por medio de este notebook emular un proceso similar agregando las ventajas que nos representan las SRGAN para mejorar la resolución de las fotos obtenidas, y poder obtener mas información a partir de fuentes de baja resolución y con alta interferencia.

</ul>

<div id='id2' />

## **Obtención de los datos**
<ul>
  <li>2.1 Obtención de datos observacionales planetarios y lunares</li>
  
Para la obtención del dataset con las imagenes de los cuerpos celestes a trabajar (Luna, Saturno y Jupiter) se utilizaron 2 diferentes telescopios, un Telescopio reflector PowerSeeker 114mm EQ montado con una cámara canon EOS Rebel T5 (Diego Villalba), junto a un telescopio Orion Apex de 127 mm de tipo Maksutov-Cassegrain, con una camara planetaria ZWO ASI con resolución full HD (Ing. Alfredo García Flores).

Se obtuvieron 8 videos de la luna, de los cuales 5 de ellos fuerón sólo enfocando una parte de la luna y los otros 3 enfocando a la luna de manera completa; por otro lado, de Saturno se tomó un sólo video, haciendo lo mismo con Jupiter, esto mediante un setup como el de la imagen.  
![Setup](https://10minuteastronomy.files.wordpress.com/2012/07/apex-127-and-travel-scope-70.jpg)


Posterior a lo anterior, para poder obtener el conjunto de datos utilizamos PIPP (Planetary Imaging PreProcessor), una aplicación de Windows diseñada para preprocesar imágenes planetarias, donde se puede recortar cada cuadro de imagen y seleccionar solo los cuadros de mejor calidad para reducir los requisitos de procesamiento y memoria empleada por nuestra red neuronal.

![PIPP](https://img.informer.com/pf/pipp-v2.5-main-window-outlook.png)

![PIPP_R](https://deepskyworkflows.com/assets/images/2022-02-20/pippcamera1.jpg)

Por otro lado, se planteó una estategia para llevar a cabo nuestras imagenes de procesamiento planetaria; como primera parte, se tomaron las mejores 1200 imagenes de ambos planetas y del satelite natural de la tierra, después, se tomaron las mejores 100 para contrastar el resultado al hacerle el proceso de stacking, y asi obtener las muestras a mejorar en nuestras redes neuronales.

  <li>2.2 Esecificaciones del equipo utilizado.</li>
    <ul>
      <li>2.2.1 Telescopio PowerSeeker 114 EQ</li>
El telescopio PowerSeeker 114 EQ es un modelo de telescopio reflector Newtoniano con una apertura de 114 mm y una longitud focal de 900 mm. Viene con una montura ecuatorial EQ que permite un seguimiento preciso de los objetos astronómicos. Incluye oculares, un buscador de punto rojo y accesorios adicionales.
      <li>2.2.2 Cámara Canon EOS Rebel T5</li>
Cuenta con un sensor de 18 megapíxeles, un sistema de enfoque automático de 9 puntos y una velocidad de disparo continuo de hasta 3 fotogramas por segundo. Puede grabar video Full HD y ofrece opciones de conectividad como USB y HDMI. Es una cámara versátil y fácil de usar para aquellos que desean iniciar su experiencia en la fotografía.
      <li>2.2.3 Telescopio Orion Apex 127mm Maksutov-Cassegrain </li>
Cuenta con una apertura de 127 mm y una distancia focal de 1540 mm, ofrece imágenes nítidas y detalladas de objetos celestes. Su diseño óptico Maksutov-Cassegrain combina un espejo cóncavo y una lente correctora, lo que resulta en un sistema compacto y de alta calidad óptica.

cuenta con un buscador de punto rojo que ayuda a alinear el telescopio con los objetos deseados en el cielo. Además, su rosca de montaje para adaptadores de cámara permite la conexión de una cámara DSLR para la astrofotografía, lo que brinda la oportunidad de capturar imágenes impresionantes del universo.
    </ul>
  </li>
</ul>


