# Essential Commands

When starting an Attack and Defense (AD) scenario, the first step is to identify the services running within the Vulnerable VM.

## Identifying Docker Services

In the case of Docker, there are two common ways to identify running services:

### 1. Listing Docker Containers

To list all Docker containers (including stopped ones) running on the machine along with their respective ports, use the following command:

```bash
docker ps -a
```

### 2. Inspect docker-compose file
Another method involves inspecting services defined in a docker-compose.yml file. This file specifies the configuration of Docker services and their dependencies.

To inspect the services defined in a docker-compose.yml file and view their configuration details, use the following command:
```bash
docker-compose config
```

## Making changes permanent
After you identified services and find a patch to it you need to make permanent these changes. In order to do this when you modify the code of a web server within a Docker container you need to create a new Docker image with the incorporated modifications.

1. **Modify the Code**: Edit the necessary files inside the Docker container (PHP scripts, python files..)

2. **Create a New Dockerfile**: Create a new Dockerfile in your project directory to define the customized Docker image. Make sure to include the necessary instructions to copy the modified files into the image.

   Example Dockerfile:
   ```Dockerfile
   FROM nginx:latest
   COPY /path/to/modified/files /usr/share/nginx/html
   ```

3. **Build the changes**:
   In your `docker-compose.yml` file, ensure that the service references the updated Dockerfile. Use the `build` directive to specify the build context (directory containing the Dockerfile) for the service.

   Example `docker-compose.yml` snippet:

   ```yaml
   version: "3"
   services:
     web:
       build:
         context: .
         dockerfile: Dockerfile
       ports:
         - "80:80"

   ```

   then you need to rebuild this compositor:

   ```
   docker-compose up --build -d
   ```
   The --build flag ensures that docker-compose rebuilds the service images before recreating the containers, and the -d flag runs the containers in detached mode (background).Verify that the modifications applied in the updated Dockerfile are reflected in the running containers after this process.
