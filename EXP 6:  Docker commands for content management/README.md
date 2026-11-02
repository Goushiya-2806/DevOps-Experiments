# EXPERIMENT 6: EXPLORE DOCKER COMMANDS FOR CONTENT MANAGEMENT

AIM:

To explore and execute Docker commands for content management, including image management, container lifecycle, file transfer, logs, inspection, and volume management.

## Software Requirements

1. Docker installed on the system.
2. Ubuntu Operating System.
3. Linux Terminal.
4. Internet connection.

## PROCEDURE

### Step 1: Check Docker is Working

Check the Docker version:

```
docker --version
```

Display Docker system information:

```
docker info
```

### Step 2: Image Management

Download the Ubuntu image from Docker Hub:

```
docker pull ubuntu
```

List all downloaded images:

```
docker images
```

Remove a Docker image:

```
docker rmi <image_id>
```

### Step 3: Container Lifecycle Management

Create and start an Ubuntu container in interactive mode:

```
docker run -it ubuntu bash
```

List running containers:

```
docker ps
```

List all containers, including stopped containers:

```
docker ps -a
```

Stop a running container:

```
docker stop <container_id>
```

Start a stopped container:

```
docker start <container_id>
```

Remove a container:

```
docker rm <container_id>
```

### Step 4: Working with Content Inside Containers

Enter a running container:

```
docker exec -it <container_id> bash
```

Copy a file from the host system into the container:

```
docker cp file.txt <container_id>:/tmp/
```

Copy a file from the container to the host system:

```
docker cp <container_id>:/tmp/file.txt .
```

### Step 5: Logs and Inspection

Display container logs:

```
docker logs <container_id>
```

Display detailed information about a container:

```
docker inspect <container_id>
```

### Step 6: Volume Management

Create a Docker volume:

```
docker volume create mydata
```

Run an Ubuntu container with the volume mounted:

```
docker run -it -v mydata:/app/data ubuntu bash
```

List all Docker volumes:

```
docker volume ls
```

Display detailed information about a volume:

```
docker volume inspect mydata
```

## OUTPUT

The following operations were performed successfully:

1. Checked Docker version and system information.
2. Downloaded and listed Ubuntu images.
3. Created, started, stopped, and removed containers.
4. Copied files between the host system and containers.
5. Viewed container logs and inspected container details.
6. Created and inspected Docker volumes.

## RESULT

Thus, Docker commands for content management were successfully explored and executed. Image management, container lifecycle management, file transfer, logs, inspection, and volume management were demonstrated.

## Important Commands for Lab Exam

| Command                      | Purpose                    |
| ---------------------------- | -------------------------- |
| `docker --version`           | Check Docker version       |
| `docker pull ubuntu`         | Download an image          |
| `docker images`              | List images                |
| `docker run -it ubuntu bash` | Create and run a container |
| `docker ps`                  | List running containers    |
| `docker ps -a`               | List all containers        |
| `docker stop`                | Stop a container           |
| `docker start`               | Start a container          |
| `docker rm`                  | Remove a container         |
| `docker cp`                  | Copy files                 |
| `docker logs`                | View container logs        |
| `docker inspect`             | View container details     |
| `docker volume create`       | Create a volume            |
| `docker volume ls`           | List volumes               |

Important viva questions

1. What is Docker?\
   Docker is an open-source platform used to create, deploy, and manage applications inside containers.
2. What is a Docker image?\
   A Docker image is a read-only template used to create containers.
3. What is a Docker container?\
   A container is a running instance of a Docker image.
4. What is Docker Hub?\
   Docker Hub is a cloud-based registry used to store and download Docker images.
5. What is a Docker volume?\
   A Docker volume is used to store data permanently, even if a container is removed.
6. Difference between image and container?\
   An image is a template, whereas a container is an instance created from that image.

Note: Replace `<image_id>` and `<container_id>` with actual IDs displayed by Docker. Do not type the angle brackets.
