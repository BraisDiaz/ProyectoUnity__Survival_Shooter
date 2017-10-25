# ProyectoUnity_Survival_Shooter
A game we made with Unity 5.

------------------------------------------------------- DESCRIPCIÓN GENERAL --------------------------------------------------------
Se trata de un shooter en 3D con una vista en tercera persona desde una perspectiva elevada y algo alejada del jugador. La historia
del mismo se basa en que nuestro personaje es un niño, que se despierta por la noche en su habitación, en la que sus peluches cobran
vida como si fueran zombies y lo persiguen intentando matarlo. Él, armado con un AK-47 les dispara para defenderse. La acción está
ambientada en la habitación del personaje, con diferentes gameObjects a su alrededor (juguetes, cómodas, etc) que funcionan como
decoración ambiental.

La cámara se mueve de forma horizontal y vertical cuando el personaje se desplaza de cualquiera de estas formas, manteníendolo en el
centro de la misma. Los enemigos, mediante un nav mesh agent, persiguen a nuestro jugador por todo el mapa esquivando los distintos
obstáculos decorativos, y atacándolo cuando entran en contacto con él. 

La HUD muestra una barra de vida con un corazón y un marcador en la parte alta de la pantalla que contabiliza los puntos que vamos 
consiguiendo al eliminar enemigos (cada tipo de enemigo tiene un valor distinto para la puntuación, así como un mayor daño de ataque,
distinta velocidad, animaciones, etc).

También dispone de los clips de audio correspondientes a la música de fondo del juego, disparos del arma, daño producido por enemigos
y daño producido a enemigos, muerte de un enemigo o de nuestro jugador (si nuestro personaje muere el juego termina y vuelve a empezar
de 0), etc.

A la hora de realizarlo he ido siguiendo uno de los distintos tutoriales que pone a nuestra disposición Unity, así como los assets del
mismo que he descargado desde la Asset Store de la aplicación. Adjunto documentación del tutorial, desde el que podemos acceder a los
vídeos y a las explicaciones ----> https://unity3d.com/es/learn/tutorials/projects/survival-shooter-tutorial
------------------------------------------- Exposición juego Unity Survival Shooter 3D ---------------------------------------------
Temas a tratar en concreto:
-Sistema de partículas de Unity (Particle System).
     Partiendo de un foco emisor, en este caso en concreto la parte final del arma del jugador ("Player"), se emiten una cantidad de partículas (podemos entender por partícula una pequeña imagen o mesh, y cada una de ellas forma parte de un conjunto, siendo una pequeña parte del mismo, por ejemplo, una parte de una nube de humo, y al actuar todas juntas conforman el efecto del mismo).
     Mediante el Particle System podemos configurar diferentes opciones como la Duración de las mismas (lifetime, tiempo de vida hasta que desaparecen), el retardo desde su activación hasta que se materializan y se pueden ver, la velocidad a la que empiezan, el tamaño en 3D de la representación, el color de las mismas, el número de partículas (emission rate), etc.
     //Hago una demostración cambiando algunas de esas opciones y mostrándolas.
     Adjunto documentación -->   https://docs.unity3d.com/es/current/Manual/PartSysWhatIs.html
-Funcionamiento general del disparo de un arma (Line Renderer, Physics Raycaster luces, sombras etc).
     Para llevar a cabo el efecto de un disparo, además del humo que representa la explosión propia del mismo, son necesarios otros medios. 
     Uno de ellos es el Line Renderer, que aplicado también a la parte final del arma, nos permite dibujar una línea entre dos puntos del espacio (no una línea como tal dado que utiliza un vector en 3D, pudiendo definir el tamaño de la misma, ancho, etc. Así mediante un Script podemos manejar el evento de activar el Line Renderer tras haber pulsado el botón de disparar, apareciendo la línea y desapareciendo tras un breve periodo de tiempo.
     En segundo lugar debemos tener en cuenta los Physics Raycaster, para entenderlo de una manera simple, gracias a ellos podemos obtener datos del impacto de nuestro "haz de luz", que sería el Line Renderer cuando colisiona contra un GameObject y utilizarlos para, por ejemplo, reducir la vida del enemigo.
     Por último, tenemos el componente Light para modificar las luces del entorno del arma. Podemos configurar el tipo de luz que se emite, Point (desde el punto de emisión), Directional (hace el efecto en toda la pantalla, como si fuera un relámpago) y Spot (emisión de luz con el efecto de una linterna). También podemos modificar el color de la misma, su intensidad y el rango de emisión, así como las sombras que se producen por el efecto de la luz.
     Adjunto documentación --> 
     https://docs.unity3d.com/es/current/Manual/class-LineRenderer.html
     https://docs.unity3d.com/es/current/Manual/script-PhysicsRaycaster.html
-Explicación general del sistema de navegación de la IA (Nav Mesh Agent).
     Aplicamos este componente para dotar de una especie de "vida propia" a un personaje del juego, en nuestro caso a los enemigos. En primer lugar podemos elegir una serie de opciones como la velocidad, aceleración o distancia a la que frenarían al encontrarse un GameObject con el identificador static, que son los que reconoce como elementos "muertos" del espacio de juego y los considera obstáculos, o bien al acercarse al objetivo final (en nuestro caso el jugador). De esta forma podemos cambiar el tamaño que reconoce de los mismos (lo ideal es darle un tamaño igual o algo mayor al de nuestro personaje al que aplicamos el Nav Mesh Agent, con el fin de que no haya problemas a la hora de interactuar con ellos), lo mismo con el radio de los obstáculos.
     Como dato es bueno tener en cuenta que con este sistema podemos usar la API de scripting del Nav Mesh Agent para utilizar el recurso de Pathfinding, por lo que los personajes no se quedarían perdidos chocando contra un obstáculo, sino que buscarían un camino hacia su objetivo.
     Adjunto documentación --> 
     https://docs.unity3d.com/es/current/Manual/class-NavMeshAgent.html
Y con esto termina la exposición.
