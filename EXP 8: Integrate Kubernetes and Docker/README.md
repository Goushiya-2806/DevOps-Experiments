# PROGRAM 1: INTEGRATE KUBERNETES AND DOCKER

## 1. AIM

To integrate Docker with Kubernetes using Minikube and deploy a simple HTML application using Kubernetes Deployment and Service.

## 2. SOFTWARE REQUIREMENTS

1. Visual Studio Code.
2. Ubuntu (WSL).
3. Docker Desktop.
4. Kubernetes (Minikube).
5. kubectl.

## 3. PROCEDURE

### Understanding the Architecture

The integration of Docker and Kubernetes follows this flow:

HTML Application

Docker Image

Kubernetes Deployment

Pods

Kubernetes Service

Web Browser

Explanation:

- Docker: Creates the application image.
- Kubernetes: Manages application containers.
- Minikube: Runs a local Kubernetes cluster.
- kubectl: Communicates with Kubernetes.
- Deployment: Creates and manages Pods.
- Service: Exposes the application.

# PART A: INSTALLATION

### Step 1: Open Ubuntu in VS Code

If you are using Windows:

1. Install Ubuntu through WSL.
2. Install Docker Desktop.
3. Enable WSL 2 integration in Docker Desktop.
4. Install the VS Code extension WSL.
5. Open Ubuntu terminal in VS Code.

Open the integrated terminal using:

```
Ctrl + Shift + ~
```

Important: Select Ubuntu (WSL) as your terminal, not Windows PowerShell. The following installation commands are Linux commands.

### Step 2: Install Docker

Execute:

```
sudo apt update
```

Install Docker:

```
sudo apt install docker.io -y
```

Start Docker:

```
sudo systemctl enable --now docker
```

Check Docker:

```
docker --version
```

Expected Output:

```
Docker version 28.x.x
```

Note: If you are using Docker Desktop with WSL integration, Docker is already provided by Docker Desktop. You generally do not need to install a second Docker Engine inside Ubuntu.

### Step 3: Install kubectl

Execute:

```
sudo snap install kubectl --classic
```

Verify:

```
kubectl version --client
```

Expected Output:

```
Client Version: v1.x.x
```

### Step 4: Install Minikube

Download Minikube:

```
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
```

Install:

```
sudo install minikube-linux-amd64 /usr/local/bin/minikube
```

Verify:

```
minikube version
```

Expected Output:

```
minikube version: v1.x.x
```

### Step 5: Start Kubernetes

Execute:

```
minikube start --driver=docker
```

Wait until Minikube starts successfully.

Verify Kubernetes:

```
kubectl get nodes
```

Expected Output:

```
NAME       STATUS   ROLES           AGE   VERSION
minikube   Ready    control-plane   1m    v1.x.x
```

If a Docker permission error occurs, configure Docker access according to your Docker installation.

# PART B: CREATE DOCKER APPLICATION

### Step 6: Create Project Folder

Execute:

```
mkdir ~/k8s-docker
cd ~/k8s-docker
```

Open this folder in VS Code:

```
code .
```

Your project folder will be:

```
k8s-docker/
```

### Step 7: Create index.html

In VS Code:

1. Click New File.
2. Name it `index.html`.
3. Paste the following code.

Program: index.html

```
<html>
<body>

<h1>Hello from Docker and Kubernetes!</h1>

<p>DevOps Lab Experiment</p>

</body>
</html>
```

Save using `Ctrl + S`.

### Step 8: Create Dockerfile

Create another file named:

`Dockerfile`

Paste the following code:

Program: Dockerfile

```
FROM nginx:alpine

COPY index.html /usr/share/nginx/html/index.html

EXPOSE 80
```

Save the file.

Explanation:

| Instruction         | Meaning                         |
| ------------------- | ------------------------------- |
| `FROM nginx:alpine` | Uses lightweight Nginx image    |
| `COPY`              | Copies HTML file into container |
| `EXPOSE 80`         | Indicates application port      |

# PART C: BUILD DOCKER IMAGE

### Step 9: Build Docker Image

Execute:

```
minikube image build -t myapp:v1 .
```

This builds the Docker image directly into Minikube's image environment.

Expected Output:

```
Successfully built ...
Successfully tagged myapp:v1
```

### Step 10: Verify Docker Image

Execute:

```
minikube image ls
```

You should find:

```
myapp:v1
```

# PART D: KUBERNETES DEPLOYMENT

### Step 11: Create deployment.yaml

In VS Code, create a new file named:

`deployment.yaml`

Paste the following code carefully. YAML indentation is important!

Program: deployment.yaml

```
apiVersion: apps/v1
kind: Deployment

metadata:
  name: myapp

spec:
  replicas: 2

  selector:
    matchLabels:
      app: myapp

  template:
    metadata:
      labels:
        app: myapp

    spec:
      containers:
      - name: myapp
        image: myapp:v1
        imagePullPolicy: Never

        ports:
        - containerPort: 80
```

Save the file.

Explanation:

- `kind: Deployment` – Creates a Kubernetes Deployment.
- `replicas: 2` – Creates two application Pods.
- `image: myapp:v1` – Uses our Docker image.
- `containerPort: 80` – Application runs on port 80.
- `imagePullPolicy: Never` – Uses the locally available image instead of downloading it.

### Step 12: Create Deployment

Execute:

```
kubectl apply -f deployment.yaml
```

Expected Output:

```
deployment.apps/myapp created
```

### Step 13: Check Pods

Execute:

```
kubectl get pods
```

Expected Output:

```
NAME                     READY   STATUS
myapp-xxxxxxxxxx-xxxxx   1/1     Running
myapp-xxxxxxxxxx-yyyyy   1/1     Running
```

Two Pods should be running.

# PART E: CREATE KUBERNETES SERVICE

### Step 14: Create service.yaml

Create another file named:

`service.yaml`

Paste the following code:

Program: service.yaml

```
apiVersion: v1
kind: Service

metadata:
  name: myapp-service

spec:
  type: NodePort

  selector:
    app: myapp

  ports:
  - port: 80
    targetPort: 80
    nodePort: 30080
```

Save the file.

Explanation:

- `kind: Service` – Creates a Kubernetes Service.
- `type: NodePort` – Exposes the application through a node port.
- `port: 80` – Service port.
- `targetPort: 80` – Container port.
- `nodePort: 30080` – External access port.

### Step 15: Create Service

Execute:

```
kubectl apply -f service.yaml
```

Expected Output:

```
service/myapp-service created
```

### Step 16: Verify Service

Execute:

```
kubectl get services
```

Expected Output:

```
NAME            TYPE       CLUSTER-IP      PORT(S)
myapp-service   NodePort   10.96.x.x       80:30080/TCP
```

# PART F: ACCESS THE APPLICATION

### Step 17: Get Application URL

Execute:

```
minikube service myapp-service --url
```

It displays a URL similar to:

```
http://192.168.49.2:30080
```

The actual URL may differ.

### Step 18: Test Application

Execute:

```
curl http://$(minikube ip):30080
```

Expected Output:

```
<html>
<body>

<h1>Hello from Docker and Kubernetes!</h1>

<p>DevOps Lab Experiment</p>

</body>
</html>
```

Open the URL displayed in Step 17 in your browser.

You should see:

Browser Output

# Hello from Docker and Kubernetes!

DevOps Lab Experiment

# PART G: VERIFY KUBERNETES

Execute the following commands.

1\. Check Deployment

```
kubectl get deployments
```

2\. Check Pods

```
kubectl get pods
```

3\. Check Services

```
kubectl get svc
```

All resources should be running successfully.

# PART H: CLEANUP

After completing the experiment, execute:

Delete Service:

```
kubectl delete -f service.yaml
```

Delete Deployment:

```
kubectl delete -f deployment.yaml
```

Stop Minikube:

```
minikube stop
```

# 4. COMPLETE PROJECT STRUCTURE

Your VS Code Explorer should look like this:

```
k8s-docker/
│
├── index.html
│
├── Dockerfile
│
├── deployment.yaml
│
└── service.yaml
```

# 5. OUTPUT

The following operations are performed successfully:

1. Docker is installed and verified.
2. kubectl is installed and configured.
3. Minikube Kubernetes cluster is started.
4. HTML application is created.
5. Dockerfile is created.
6. Docker image is built successfully.
7. Kubernetes Deployment is created with two replicas.
8. Two Pods are created and verified.
9. Kubernetes Service is created using NodePort.
10. Application is accessed through the web browser.

# 6. RESULT

Thus, Docker was successfully integrated with Kubernetes using Minikube. A simple HTML application was containerized using Docker, deployed using Kubernetes Deployment, and exposed using Kubernetes Service. The application was accessed successfully through the web browser.

# Important Commands for Lab Exam

| Command                                | Purpose                  |
| -------------------------------------- | ------------------------ |
| `docker --version`                     | Check Docker version     |
| `kubectl version --client`             | Check kubectl version    |
| `minikube version`                     | Check Minikube version   |
| `minikube start --driver=docker`       | Start Kubernetes cluster |
| `kubectl get nodes`                    | Display cluster nodes    |
| `minikube image build -t myapp:v1 .`   | Build Docker image       |
| `minikube image ls`                    | List Minikube images     |
| `kubectl apply -f deployment.yaml`     | Create Deployment        |
| `kubectl get pods`                     | Display Pods             |
| `kubectl apply -f service.yaml`        | Create Service           |
| `kubectl get svc`                      | Display Services         |
| `minikube service myapp-service --url` | Get application URL      |
| `minikube stop`                        | Stop Minikube            |

# Important Viva Questions and Answers

1\. What is Docker?

Docker is an open-source platform used to create, deploy, and manage applications inside containers.

2\. What is Kubernetes?

Kubernetes is an open-source container orchestration platform used to automate deployment, scaling, and management of containerized applications.

3\. What is Minikube?

Minikube is a tool that runs a local Kubernetes cluster on a computer.

4\. What is kubectl?

kubectl is a command-line tool used to communicate with and manage Kubernetes clusters.

5\. What is a Pod?

A Pod is the smallest deployable unit in Kubernetes. It contains one or more containers.

6\. What is a Deployment?

A Deployment manages Pods and maintains the required number of replicas.

7\. What is a Kubernetes Service?

A Service exposes an application running inside Pods and allows access to it.

8\. What is NodePort?

NodePort is a Kubernetes Service type that exposes an application through a port on the cluster node.

9\. What is a Docker image?

A Docker image is a read-only template used to create containers.

10\. Why are two replicas used?

Two replicas create two Pods to improve availability and maintain the desired number of application instances.

11\. What is Nginx?

Nginx is a web server used to serve HTML pages and other web content.

12\. What is the purpose of a Dockerfile?

A Dockerfile contains instructions to build a Docker image.

Complete lab write-up

Important practical note: The commands and YAML above follow your supplied lab material. In a Windows + WSL setup, Docker Desktop must be running with WSL integration enabled. Also, `minikube service --url` may provide a URL that needs to remain accessible through the Minikube tunnel or local networking, depending on your setup. The expected outputs are examples; actual IP addresses, versions, Pod names and IDs will differ.
