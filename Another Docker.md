# Docker

### What is Docker?
>An open-source project that automates the deployment of sofware applications inside containers by providing an additional layer of abstraction and automation of OS-level virtualization on linux.

__In simpler words:__
Docker is a tool that allows developers, sys-admins etc. to easily deploy their applications in a sandbox (containers) to run on the host operating system. The key benefit of Docker is that it allows users to package an application with all of its dependencies into a standardized unit for software development.

### What are containers?

Containers take the approach of leveraging the low-level mechanics of the host operating system, containers provide most of the isolation of virtual machines at a fraction of computing power.

### Why use containers?
Containers offer a logical packaging mechanism in which applications can be abstracted from the environment in which they actually run. This decoupling allows container-based applications to be deployed easily and consistently, regardless of whether the target environment is a private data center, the public cloud, or even a developer’s personal laptop. 

### Webapps with Docker
Running a simple static website. The process is: pull a Docker image from Docker Hub, run the container and run a webserver.

```
docker run --rm prakhar1989/static-site
```
This command will fetch the image from the registry and then run the image. After it will appear this message on the terminal: `Nginx is running...`. In this case, the client is not exposing any ports so we need to re-run the docker run command to publish ports:

```
docker run -d -P --name static-site prakhar1989/static-site
```
In the above command, -d will detach our terminal, -P will publish all exposed ports to random ports and finally --name corresponds to a name we want to give. This is called detached mode.

```
docker port static-site
```

You can open http://localhost:32769 in your browser.

You can also specify a custom port to which the client will forward connections to the container.
```
docker run -p 8888:80 prakhar1989/static-site
```

### Dockerfile
A Dockerfile is a simple text-file that contains a list of commands that the Docker client calls while creating an image. It's a simple way to automate the image creation process. The best part is that the commands you write in a Dockerfile are almost identical to their equivalent Linux commands. This means you don't really have to learn new syntax to create your own dockerfiles.

The `docker build` command does the heavy-lifting of creating a Docker image from a Dockerfile.

Run `docker images` and see if your image shows. The last step in this section is to run the image and see if it actually works:
```
$ docker run -p 8888:5000 prakhar1989/catnip
 * Running on http://0.0.0.0:5000/ (Press CTRL+C to quit)
```
The command we just ran used port 5000 for the server inside the container, and exposed this externally on port 8888. 

## Commands
- `docker images`: List images
- `docker pull busybox`: Fetch image from Docker registry
- `docker run busybox echo "hello from busybox"`: Run command on container
- `docker ps`: Show all the containers that are currently running
- `docker ps -a`: Show all the containers status
- `docker run -it busybox sh`: Attache an interactive tty in the container
- `docker rm 305297d7a235 ff0a5c3750b9`: Delete containers
- `docker rm $(docker ps -a -q -f status=exited)`: Delete multiple exited containers
   - -q flag, only returns the numeric IDs
   - -f filters output based on conditions provided
- `docker container prune`: Delete all stopped containers
- `docker rmi`: Delete all stopped containers
- `docker run --rm prakhar1989/static-site`: Automatically removes the container when it exits
- `docker run -d -P --name static-site prakhar1989/static-site`: Run container, Detach the terminal, Publish all exposed ports to random ports and Gives a name 
- `docker port [CONTAINER]`: Show ports
- `docker run -p 8888:80 prakhar1989/static-site`: Specify a custom port to which the client will forward connections to the container
- `docker stop static-site`: Stop container
- `docker build`: Create a Docker image from a Dockerfile
