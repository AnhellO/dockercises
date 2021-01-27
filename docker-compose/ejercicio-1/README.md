# Ejercicio 1

Crea un archivo `docker-compose.yml` que ejecute 4 contenedores:

- El **1er contenedor** ejecutará un servidor de [`MongoDB`](https://hub.docker.com/_/mongo) y su nombre deberá de ser `mongo_compose`
- El **2do contenedor** ejecutará un cliente de [`Mongo Express`](https://hub.docker.com/_/mongo-express) el cual se llame `mexpress_compose`, y el cual se conectará al contenedor `mongo_compose` creado en el punto anterior. Este contenedor fungirá como el DBMS de la aplicación. Otro requisito más es que este cliente tiene que estar protegido por medio de las siguientes credenciales:
  - Usuario: `DASistemas`
  - Password: `ex-especial567`
- El **3er contenedor** ejecutará un programa de `GO` que lleve a cabo lo siguiente:
  - Que lea el archivo XML [`people`](people.xml)
  - Que modele/mappee los nodos de `<person>` con una estructura de `Persona`, de tal manera que cada nodo del `XML` pueda ser representado con una instancia de la estructura de `Persona`
  - Que guarde cada nodo de `<person>` en la base de datos de `MongoDB` del **1er contenedor**. Cada nodo tendrá que ser un registro por separado, pero todos estos registros pueden vivir en una sola [colección (tabla)](https://docs.mongodb.com/manual/core/databases-and-collections/) de `Mongo`
  - Asegúrate de construir el respectivo `Dockerfile` necesario para esta imagen, y de instalar todas las dependencias necesarias en el mismo
- El **4to contenedor** ejecutará un programa de `GO` que lleve a cabo lo siguiente:
  - Levantará una pequeña "`API`" que mostrará todos los registros guardados desde el `XML` a través del endpoint/recurso de `/people`, por lo tanto tendrá que conectarse al **1er contenedor** de `Mongo`, de tal manera que pueda acceder a los registros de la colección. Estos registros tendrán que ser servidos en formato `JSON` y la API tendrá que funcionar por medio de [`GO Chi`](https://github.com/go-chi/chi)
  - Aparte del endpoint/recurso de `/people`, tendremos que agregar otro endpoint/recurso que nos muestre un JSON con la información en particular para cada persona, y que sea accesible por medio de un nuevo endpoint/recurso con la forma `/people/{id}`, en donde `{id}` es igual al ID del registro en la BD
  - Asegúrate de construir el respectivo `Dockerfile` necesario para esta imagen, y de instalar todas las dependencias necesarias en el mismo
  - Finalmente, este contenedor en particular tendrá que ser ejecutado en modo "_daemonizado_", y deberá de estar accesible a través del puerto `7777` de tu máquina. Asegúrate de verificar que funciona de manera correcta :wink:

Recuerda que **todo debe de funcionar** por medio de `docker-compose`, es decir, nada debe de hacerse manualmente ni instalando algo en el equipo host.
