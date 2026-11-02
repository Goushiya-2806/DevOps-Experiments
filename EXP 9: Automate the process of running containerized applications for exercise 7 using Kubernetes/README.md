
# EXPERIMENT 7: AUTOMATE THE PROCESS OF RUNNING CONTAINERIZED APPLICATIONS USING KUBERNETES

## 1. AIM

To automate the process of running containerized applications using Kubernetes by creating a Docker image, deploying the application using Kubernetes Deployment, exposing it through a Service, and scaling the application using multiple Pods.

## 2. SOFTWARE REQUIREMENTS

1. Visual Studio Code.
2. Windows Operating System.
3. Ubuntu (WSL).
4. Docker Desktop.
5. Kubernetes (Minikube).
6. kubectl.
7. Google Chrome Web Browser.

## 3. PROCEDURE

### Step 1: Create a Project Folder

1. Open Visual Studio Code.
2. Select File → Open Folder.
3. Create a folder named `docker-app`.
4. Open the folder.

### Step 2: Create HTML File

1. Create a new file named `index.html`.
2. Enter the following HTML code.
3. Save the file using `Ctrl + S`.

Program: index.html

```
<!DOCTYPE html>
<html>
<head>
    <title>Docker Application</title>
</head>
<body>
    <h1>Hello from Docker!</h1>
    <p>Application running inside Kubernetes pods.</p>
</body>
</html>
```

### Step 3: Create Dockerfile

1. Create another file named `Dockerfile` without any extension.
2. Enter the following code.
3. Save the file.

Program: Dockerfile

```
FROM nginx:alpine
COPY index.html /usr/share/nginx/html/index.html
EXPOSE 80
```

Explanation:

- `FROM nginx:alpine` – Uses a lightweight Nginx base image.
- `COPY` – Copies the HTML file into the Nginx web server directory.
- `EXPOSE 80` – Indicates that the application uses port 80.

### Step 4: Open VS Code Terminal

1. Select Terminal → New Terminal.
2. Select Ubuntu (WSL) terminal.
3. Make sure the terminal is inside the `docker-app` folder.

Press:

```
Ctrl + ~
```

### Step 5: Check Docker

Execute:

```
docker --version
```

Expected Output:

```
Docker version 28.x.x
```

### Step 6: Build Docker Image

Execute:

```
docker build -t mywebapp:v1 .
```

Explanation:

- `docker build` – Builds a Docker image.
- `-t mywebapp:v1` – Assigns the image name and version.
- `.` – Specifies the current directory as the build context.

Expected Output:

```
Successfully tagged mywebapp:v1
```

### Step 7: Run Docker Container

Execute:

```
docker run -d -p 8080:80 --name webcontainer mywebapp:v1
```

Explanation:

- `docker run` – Creates and starts a container.
- `-d` – Runs the container in the background.
- `-p 8080:80` – Maps host port 8080 to container port 80.
- `--name webcontainer` – Assigns a name to the container.
- `mywebapp:v1` – Specifies the Docker image.

### Step 8: Check Running Container

Execute:

```
docker ps
```

Expected Output:

```
CONTAINER ID   IMAGE         STATUS
xxxxxxxx       mywebapp:v1   Up
```

### Step 9: Test Application

Open Google Chrome and enter:

```
http://localhost:8080
```

Expected Browser Output:

# Hello from Docker!

Application running inside Kubernetes pods.

# PART B: START KUBERNETES

### Step 10: Start Minikube

Execute:

```
minikube start --driver=docker
```

Wait until Minikube starts successfully.

### Step 11: Check Kubernetes Node

Execute:

```
kubectl get nodes
```

Expected Output:

```
NAME       STATUS   ROLES
minikube   Ready    control-plane
```

This confirms that the Kubernetes cluster is running successfully.

# PART C: DEPLOY APPLICATION

### Step 12: Build Image in Minikube

Make sure your terminal is inside the `docker-app` folder.

Execute:

```
minikube image build -t mywebapp:v1 .
```

This builds the Docker image inside Minikube's image environment.

### Step 13: Create Kubernetes Deployment

Execute:

```
kubectl create deployment mywebapp --image=mywebapp:v1
```

Expected Output:

```
deployment.apps/mywebapp created
```

### Step 14: Configure Image Pull Policy

Execute the following command:

```
kubectl patch deployment mywebapp -p '{"spec":{"template":{"spec":{"containers":[{"name":"mywebapp","image":"mywebapp:v1","imagePullPolicy":"Never"}]}}}}'
```

This configures Kubernetes to use the locally available Docker image instead of downloading it.

### Step 15: Create Two Replicas

Execute:

```
kubectl scale deployment mywebapp --replicas=2
```

This creates two application Pods.

### Step 16: Check Deployment

Execute:

```
kubectl get deployments
```

Expected Output:

```
NAME       READY   UP-TO-DATE   AVAILABLE
mywebapp   2/2     2            2
```

This indicates that both replicas are running successfully.

### Step 17: Check Pods

Execute:

```
kubectl get pods
```

Expected Output:

```
NAME                        READY   STATUS
mywebapp-xxxxxxxxxx-xxxxx   1/1     Running
mywebapp-xxxxxxxxxx-yyyyy   1/1     Running
```

Two Pods should be running.

# PART D: EXPOSE APPLICATION USING KUBERNETES SERVICE

### Step 18: Create Kubernetes Service

Execute:

```
kubectl expose deployment mywebapp --type=NodePort --port=80
```

Expected Output:

```
service/mywebapp exposed
```

### Step 19: Check Service

Execute:

```
kubectl get services
```

Expected Output:

```
NAME       TYPE       CLUSTER-IP    PORT(S)
mywebapp   NodePort   10.96.x.x     80:xxxxx/TCP
```

### Step 20: Open Application

Execute:

```
minikube service mywebapp --url
```

Copy the URL displayed and open it in Google Chrome.

Expected Browser Output:

# Hello from Docker!

Application running inside Kubernetes pods.

# PART E: DEMONSTRATE SCALING

### Step 21: Increase Replicas to Three

Execute:

```
kubectl scale deployment mywebapp --replicas=3
```

This increases the number of application Pods from two to three.

### Step 22: Check Pods

Execute:

```
kubectl get pods
```

Expected Output:

```
NAME                        READY   STATUS
mywebapp-xxxxxxxxxx-xxxxx   1/1     Running
mywebapp-xxxxxxxxxx-yyyyy   1/1     Running
mywebapp-xxxxxxxxxx-zzzzz   1/1     Running
```

This proves that Kubernetes successfully scaled the application from two Pods to three Pods.

# PART F: CLEANUP

After completing the experiment, execute the following commands.

Step 23: Delete Kubernetes Service

```
kubectl delete service mywebapp
```

Step 24: Delete Kubernetes Deployment

```
kubectl delete deployment mywebapp
```

Step 25: Stop Minikube

```
minikube stop
```

## 4. FOLDER STRUCTURE

Your VS Code project should look like this:

```
docker-app
    |
    |---- index.html
    |
    |---- Dockerfile
```

## 5. OUTPUT

The following operations are performed successfully:

1. Created a simple HTML application.
2. Created a Dockerfile.
3. Built a Docker image named `mywebapp:v1`.
4. Created and executed a Docker container.
5. Started the Kubernetes cluster using Minikube.
6. Created a Kubernetes Deployment.
7. Created two application Pods.
8. Exposed the application using NodePort Service.
9. Accessed the application through a web browser.
10. Scaled the application from two Pods to three Pods.
11. Successfully verified the running Pods and Deployment.

## 6. RESULT

Thus, the process of running containerized applications was successfully automated using Kubernetes. A Docker image was created, the application was deployed using Kubernetes Deployment, exposed using NodePort Service, and scaled from two replicas to three replicas successfully.

## 7. IMPORTANT COMMANDS FOR LAB EXAM

| Command                                                        | Purpose                  |
| -------------------------------------------------------------- | ------------------------ |
| `docker --version`                                             | Check Docker version     |
| `docker build -t mywebapp:v1 .`                                | Build Docker image       |
| `docker run -d -p 8080:80 --name webcontainer mywebapp:v1`     | Run container            |
| `docker ps`                                                    | Check running containers |
| `minikube start --driver=docker`                               | Start Kubernetes         |
| `kubectl get nodes`                                            | Check Kubernetes nodes   |
| `minikube image build -t mywebapp:v1 .`                        | Build image in Minikube  |
| `kubectl create deployment mywebapp --image=mywebapp:v1`       | Create Deployment        |
| `kubectl scale deployment mywebapp --replicas=2`               | Create two replicas      |
| `kubectl get deployments`                                      | Check Deployment         |
| `kubectl get pods`                                             | Check Pods               |
| `kubectl expose deployment mywebapp --type=NodePort --port=80` | Expose application       |
| `kubectl get services`                                         | Check Services           |
| `kubectl scale deployment mywebapp --replicas=3`               | Scale to three replicas  |
| `minikube stop`                                                | Stop Kubernetes          |

## 8. VIVA QUESTIONS AND ANSWERS

1\. What is Docker?

Docker is an open-source platform used to create, deploy, and manage applications inside containers.

2\. What is Kubernetes?

Kubernetes is an open-source container orchestration platform used to automate deployment, scaling, and management of containerized applications.

3\. What is Minikube?

Minikube is a tool used to run a local Kubernetes cluster.

4\. What is kubectl?

kubectl is a command-line tool used to communicate with Kubernetes clusters.

5\. What is a Pod?

A Pod is the smallest deployable unit in Kubernetes. It contains one or more containers.

6\. What is Deployment?

Deployment manages Pods and maintains the required number of replicas.

7\. What is a Kubernetes Service?

A Service exposes an application running inside Pods and allows access to it.

8\. What is NodePort?

NodePort exposes an application through a port on the Kubernetes node.

9\. What is scaling in Kubernetes?

Scaling is the process of increasing or decreasing the number of application replicas.

10\. What is Nginx?

Nginx is a web server used to serve HTML pages and other web content.

11\. What is a Dockerfile?

A Dockerfile contains instructions to build a Docker image.

12\. What is the purpose of replicas?

Replicas maintain multiple running instances of an application to improve availability and handle workload.

Complete Experiment 7 write-up

Important practical notes:

1. This experiment has two stages: running the application directly with Docker and deploying it using Kubernetes.
2. Build the image inside Minikube using `minikube image build` so Kubernetes can access it locally.
3. If `webcontainer` is still using host port 8080, the Kubernetes NodePort application uses a different port, so there is no conflict with that NodePort.
4. If the browser cannot open the Minikube URL, use `minikube service mywebapp --url` and keep the command/session running if your WSL setup requires a tunnel.
5. The output IDs, IP addresses, Pod names and version numbers will differ on your system.
