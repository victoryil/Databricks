# Databricks Spark

Esto es una preparación a la certificación de **DB** usando **Scala Spark**

## Arquitectura de Spark

Por la parte lógica, cada vez que enviamos una acción/trabajo de nuestro trabajo, internamente se genera un Job, que es un trabajo para determinar la acción. Dicho trabajo se divide en particiones (**Stages**) que son independiente entre si. Cada Stage esta conformado por diferentes **Task**, que siempre va ir acorde al plan de ejecución, que indica el orden en el que se va a ir ejecutando simultáneamente. 

Por la parte física, estaría el Clúster Manager que se divide en el Driver y los Executors, donde el **Driver** solicita al **Clúster** manager los recursos para ejecutar una determinada acción, una vez que los tiene, crea un plan de ejecución y le asigna los recursos que solicito y reparte entre los distintos executor, que residen en los **Worker node**. Dentro Workers Nodes, encontraremos diversas tareas en unos Cores/Slot y a medida que se va terminando cada ejecución, transformación... va trasladando la información al driver. Spark siempre que ejecuta evalúa el estado de cada proceso si falla o ve que tarda demasiado, genera un proceso en paralelo para poder cubrir esa tarea. En resumen, hace intentos en paralelo para que el usuario que esta lanzando la query, no note el error. Los **Chunk** son las particiones/ los bloques de data que se crean dentro de cada Executor. Una vez que termine cada Task, se retorna todo el conjunto al Driver para mostrar los datos 

![](.\img\spark-architecture.png)

### Aclaración

Un grupo de Task representaría un Stage

Un grupo de Stages representaría un Job

Databricks maneja diferente los Worker nodes

Los Chunks son las particiones de datos se alojan en la memoria RAM para ser procesado, cada nodo tiene su disco donde se hace las operaciones de Shuffle

Cada Ejecutor es una JVM al igual que el Driver.

La mínima unidad lógica es una Task en recurso lógico o un Slot en el recurso físico

El Driver se comunica con el cliente pero también se puede lanzar desde dentro del cluster