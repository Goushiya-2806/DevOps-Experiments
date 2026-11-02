# EXPERIMENT 7: BUILD A SIMPLE CONTAINERIZED APPLICATION USING DOCKER

## 1. AIM

To create a simple HTML application, build a Docker image, and run the application inside a Docker container.

## 2. SOFTWARE REQUIREMENTS

1. Visual Studio Code.
2. Docker Desktop.
3. Web Browser (Google Chrome).
4. Windows Operating System.

## 3. PROCEDURE

### Step 1: Create a Project Folder

1. Open Visual Studio Code.
2. Select File → Open Folder.
3. Create a folder named `docker-html-program`.
4. Open the folder in VS Code.

### Step 2: Create HTML File

1. Create a new file named `index.html`.
2. Write the following HTML code.
3. Save the file using `Ctrl + S`.

Program: index.html

```
<html>
<body>
    <h1>Hello Docker Demonstration</h1>
    <p>This is My first Docker containerized web application.</p>
</body>
</html>
```

### Step 3: Create Dockerfile

1. Create another file named `Dockerfile` without any extension.
2. Enter the following code.
3. Save the file.

Program: Dockerfile

```
FROM nginx
COPY index.html /usr/share/nginx/html/
```

Explanation:

- `FROM nginx` – Uses the Nginx base image.
- `COPY` – Copies the HTML file into the Nginx web server directory.

### Step 4: Open VS Code Terminal

1. Select Terminal → New Terminal.
2. Make sure the terminal is inside the `docker-html-program` folder.
3. Check that Docker Desktop is running.

### Step 5: Build Docker Image

Execute the following command:

```
docker build -t myhtml .
```

Explanation:

- `docker build` – Builds a Docker image.
- `-t myhtml` – Assigns the image name as `myhtml`.
- `.` – Specifies the current directory as the build context.

### Step 6: Verify Docker Image

Execute the following command:

```
docker images
```

This command displays all available Docker images.

The `myhtml` image should appear in the list.

### Step 7: Run Docker Container

Execute the following command:

```
docker run -d -p 8080:80 myhtml
```

Explanation:

- `docker run` – Creates and starts a container.
- `-d` – Runs the container in the background.
- `-p 8080:80` – Maps host port 8080 to container port 80.
- `myhtml` – Specifies the Docker image name.

### Step 8: Verify Running Container

Execute the following command:

```
docker ps
```

This command displays all currently running containers.

### Step 9: Open Application in Browser

1. Open Google Chrome.
2. Enter the following URL:

```
http://localhost:8080
```

3. Press Enter.
4. The HTML application will be displayed in the browser.

## 4. FOLDER STRUCTURE

The VS Code project should look like this:

```
docker-html-program
│
├── index.html
│
└── Dockerfile
```

## 5. EXPECTED OUTPUT

Google Chrome – localhost:8080

# Hello Docker Demonstration

This is My first Docker containerized web application.

The following output is displayed in the browser:

```
Hello Docker Demonstration

This is My first Docker containerized web application.
```

## 6. RESULT

Thus, a simple HTML application was successfully created, a Docker image was built using the Dockerfile, and the application was executed inside a Docker container using Nginx. The application was accessed successfully through the web browser at `http://localhost:8080`.

## Important Commands for Lab Exam

| Command                           | Purpose                    |
| --------------------------------- | -------------------------- |
| `docker --version`                | Check Docker version       |
| `docker build -t myhtml .`        | Build Docker image         |
| `docker images`                   | Display Docker images      |
| `docker run -d -p 8080:80 myhtml` | Run Docker container       |
| `docker ps`                       | Display running containers |
| `docker stop <container_id>`      | Stop container             |

Important: If port 8080 is already in use, use another host port, such as `8081:80`, and open `http://localhost:8081` instead.
