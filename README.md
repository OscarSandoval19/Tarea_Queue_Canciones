# Tarea_Queue_Canciones

# Como compilar la librería y commo instalar en local

Para poder compilar la libreria primero hay que registrar la estructura de datos en el repositorio local de Maven (.m2)

Ir a la carpeta: cd umg.edu.gt.data-structure.queue

Escribir en cmd: mvn clean install

Esto generará el archivo .jar y lo hará disponible para el otro proyecto que realizaremos.

# Cómo compilar el handler

Para compilar el handler nos vamos a la carpeta de "queueHandler" y arriba escribimos cmd para abrirlo en esa carpeta.

Luego usamos este comando: mvn clean package

Con eso ya estaria compilado la parte del Handler.

# Cómo ejecutar desde consola

Para ejecutarlo en consola utilizamos el siguiente comando, siempre en el cmd que tenemos abierto en la carpeta de queueHandler:

mvn exec:java -Dexec.mainClass="umg.edu.gt.data_structure.queueHandler.queueHandler.Main"

# Explicación del diseño

Para el diseño decidi usar un diseño Modular:

- Librería (queue): Esta contiene la logica de la estructura de datos QueueLinked<T>. Tuve que pasarla a generica, lo que permite almacenar cualquier objeto (Song, String, Integer).

- Consumidor (queueHandler): Es la aplicación final que conecta las funciones de la librería para gestionar la música.

# Decisiones técnicas

- Estructura de Datos: Use una Lista Simplemente Enlazada para la cola, lo cual permite inserciones (O(1)) y extracciones (O(1)) de alta eficiencia.

- Manejo de Tiempo: Usando Thread.sleep(1000) me sirvio para pausar el hilo principal de ejecución emulando la velocidad de reproducción en un contexto real.

# Cómo implementaste la prioridad

Para cumplir con la regla de "No usar PriorityQueue de Java" y "No romper el FIFO" use la técnica de Colas de Prioridad Multinivel:

- El sistema instancia dos colas independientes: highPriorityQueue y normalPriorityQueue.

- Al cargar las canciones se clasifican según su atributo priority.

- El motor de ejecución procesa de forma primordial la cola de Alta prioridad antes de pasar a la Normal.

- Esto garantiza que si dos canciones tienen la misma prioridad se respete el orden en que llegaron (FIFO).

 # Cómo manejaste la simulación de duración

No queria limitarme a imprimir solo un texto plano asi que decidi implementar un ciclo for basado en el atributo duration de cada objeto de la clase Song:

- Por cada iteración del ciclo el programa espera 1 segundo real.

- Se calcula el porcentaje de avance para renderizar una Barra de Progreso Visual [#####-----].

- Se acumula el tiempo en una variable global para mostrar el Tiempo Total Reproducido al finalizar la todas las canciones o la playlist.
