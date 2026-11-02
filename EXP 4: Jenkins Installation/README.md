# PROGRAM 4: JENKINS INSTALLATION AND SETUP, EXPLORE THE ENVIRONMENT

Aim:

To install and configure Jenkins, explore the Jenkins environment, create a new build job, execute a Java program, and check the build status.

Hardware Requirements:

1. RAM: 4 GB
2. Hard Disk: More than 50 GB

Software Requirements:

1. Java Development Kit (JDK) or Java Runtime Environment (JRE).
2. Web Browser (Google Chrome, Mozilla Firefox, or Microsoft Edge).
3. Ubuntu 18.04 Server with a non-root sudo user and firewall.

## Procedure / Steps

### Step 1: Install Jenkins

1\. Add the Jenkins repository key:

```
wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -
```

2\. Add the Jenkins repository:

```
sudo sh -c 'echo deb http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
```

3\. Update the package list:

```
sudo apt update
```

4\. Install Jenkins:

```
sudo apt install jenkins
```

### Step 2: Start Jenkins Server

Start Jenkins using the following command:

```
sudo systemctl start jenkins
```

Check the status of Jenkins:

```
sudo systemctl status jenkins
```

If Jenkins is running successfully, its status will be displayed as active.

### Step 3: Configure Jenkins

1. Open a web browser.
2. Enter the following URL:

```
http://your_server_ip:8080
```

3\. Get the initial administrator password using:

```
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

4. Copy the password and paste it into the Administrator Password field.
5. Click Continue.
6. Select Install suggested plugins.
7. Wait until all plugins are installed.

### Step 4: Create Admin User

1. Enter the administrator username.
2. Enter the password.
3. Confirm the password.
4. Enter the required details.
5. Click Save and Continue.

### Step 5: Configure Jenkins URL

1. Confirm the Jenkins URL.
2. Click Save and Finish.
3. Click Start using Jenkins.

The Jenkins Dashboard will appear.

### Step 6: Create a New Build Job

1. Log in to Jenkins.
2. Click on New Item.
3. Enter the project name.
4. Select Freestyle Project.
5. Click OK.
6. Enter the project description.

### Step 7: Configure Source Code Management

1. Open the Source Code Management section.
2. Select Git.
3. Enter the GitHub repository URL.
4. Configure the required repository details.

### Step 8: Configure Build Environment

1. Go to the Build section.
2. Click Add build step.
3. Select the appropriate command execution option.

For Linux, select Execute Shell. For Windows, select Execute Windows Batch Command.

Enter the following Java commands:

```
javac HelloWorld.java
java HelloWorld
```

### Step 9: Save and Build the Project

1. Click Apply.
2. Click Save.
3. Click Build Now.
4. A new build number will appear in Build History.
5. Click the build number.
6. Select Console Output to check the execution status.

## Step 10: Verify Output

If the Java program executes successfully, the console displays the program output and:

```
Finished: SUCCESS
```

If the build fails, check Console Output to identify and correct the errors.

## Result

Jenkins was successfully installed and configured. A new build job was created, Java source code was compiled and executed, and the build status was verified using Console Output.

Lab exam ready

Important commands to remember

| Purpose            | Command                                                  |
| ------------------ | -------------------------------------------------------- |
| Update packages    | `sudo apt update`                                        |
| Install Jenkins    | `sudo apt install jenkins`                               |
| Start Jenkins      | `sudo systemctl start jenkins`                           |
| Check status       | `sudo systemctl status jenkins`                          |
| Get admin password | `sudo cat /var/lib/jenkins/secrets/initialAdminPassword` |
| Compile Java       | `javac HelloWorld.java`                                  |
| Run Java           | `java HelloWorld`                                        |

Note: Your lab manual uses Ubuntu 18.04 and older Jenkins repository commands. For a fresh installation today, the repository key and Java requirements may need updating. The above is a simplified write-up based on your supplied manual.
