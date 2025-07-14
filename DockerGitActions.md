# Deploy automatico usando GitHub Actions

Haremos el deploy de nuestra imagen desde nuestro registro de docker hub y GitHub Actions.

- En el repositorio de nuestro proyecto, en la seccion **settings** > **Secrets and variables** > **Actions** . Creamos un **New repository secret**
  - Colocamos el nombre **DOCKER_USER** o el que sea, y en el campo secret el nombre de nuestro usuario en docker.
  - En el segundo secret que creamos llevara el nombre de **DOCKER_PASSWORD**.
    - Para obtener el valor que le asignaremos como docker_password, crearemos un token de acceso en Docker Hub. de la siguiente manera.
      1. En docker desktop seleccionamos la opcion **account settings**, Ir a **Personal access token** > **Generate new token**, le colocamos el nombre de **Github-Actions**, le asignamos los permisos de acceso **Read and write**, Dar click en **Generar**.
      2. Copiar el token generado y guardarlo ya que solo se puede visualizar una vez.
      3. Pegarlo en el valor del secret **DOCKER_PASSWORD**.
- Creamos un nuevo repositorio **Privado** o tambien publico, en docker hub
  - Le asignamoes el nombre de docker-graphql
  - Clic en **Crear**

## Seccion github Actions

- Ir a github, ir a la seccion de actions, y seleccionar Docker Image.
- Click en **Configure**, esto generará un archivo .yml
- Dar clic en **Create Commit**

### Prueba de imagen de proyecto en local

- Primero construir la imagen de docker con el comando build solamente `docker build -t richarddocker1234/docker-graphql:0.0.1`
- Ahora que hemos construido la imagen de nuestra aplicación, creamos un nuevo contenedor con nuestra imagen publicandolo con el puerto 3000 de nuestro equipo con el 3000 de ma imagen. `docker container run -dp 3000:3000 --name docker-graphql richarddocker1234/docker-graphql:0.0.1 .`
- Accedemos a la URL de nuestro navegador en https://localhost:3000/graphql , si podemos ver la aplicación entonces todo esta funcionando bien.

### GitHub Actions Steps

Editar el archivo docker-image.yml ubicado en .github > workflows.
