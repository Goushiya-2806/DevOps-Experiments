# PROGRAM 5: DEMONSTRATE CONTINUOUS INTEGRATION AND DEVELOPMENT USING JENKINS

AIM:

To demonstrate Continuous Integration and Continuous Development using Jenkins by creating a Jenkins job, connecting it to a Git repository, automating builds, and checking the build status.

## Software Requirements

1. Jenkins
2. Java JDK
3. Git
4. Ubuntu Operating System
5. Web Browser (Google Chrome / Mozilla Firefox)

## PROCEDURE

Step 1: Check Jenkins

Open the browser and enter the following URL:

```
http://localhost:8080
```

Step 2: Start Jenkins

Execute the following command:

```
sudo systemctl start jenkins
```

Step 3: Check Jenkins Status

```
sudo systemctl status jenkins
```

If Jenkins is running successfully, the status will show active.

Step 4: Create a Jenkins Job

1. Open Jenkins in the browser.
2. Click on New Item.
3. Enter the project name.
4. Select Freestyle Project.
5. Click OK.

Step 5: Configure Source Code Management

1. Go to Source Code Management.
2. Select Git.
3. Enter the Git repository URL.
4. Select the required branch.

Step 6: Configure Build

1. Go to the Build Steps section.
2. Select Execute Shell.
3. Enter the required build and test commands.

Example:

```
echo "Building the project"
echo "Testing the project"
```

Step 7: Save and Build

1. Click Save.
2. Click Build Now.
3. Jenkins starts executing the build process.

Step 8: Check Build Status

1. Open Build History.
2. Click the build number.
3. Select Console Output.
4. Check whether the build is successful or failed.

Step 9: Automate the Build

1. Open the job configuration.
2. Go to Build Triggers.
3. Enable Poll SCM.
4. Enter the schedule:

```
* * * * *
```

This checks the Git repository every minute.

Step 10: Verify CI/CD

1. Make changes to the source code.
2. Push the changes to the Git repository.
3. Jenkins checks the repository for changes.
4. If changes are detected, Jenkins automatically starts a new build.
5. Check the build result in Console Output.

## OUTPUT

If the build executes successfully, Jenkins displays:

```
Building the project
Testing the project

Finished: SUCCESS
```

[How to Install Jenkins on Ubuntu 22.04](https://images.openai.com/static-rsc-4/nuiM49Z6HPpm52v-BJFM2RRsg-xx9b6ht0pYoInZ1cMg5t3w7ZWjUX2f8uNTcgZMnEs0k8aR5aLta1TjQQk-tAZNWHASs3858zqJFxZDLgu8-iB8AZwuXrK_9PsTzOMInGhFdLv0w9YabwGPi6gjOa0faSHARmSgNiuFI2RhXpg?purpose=inline)

[howtoforge.com](https://www.howtoforge.com/tutorial/ubuntu-jenkins-automation-server/?utm_source=chatgpt.com)

## RESULT

Thus, Continuous Integration and Continuous Development were successfully demonstrated using Jenkins. A Jenkins job was created, connected to a Git repository, configured for automatic builds, and the build status was verified through Console Output.

Important for lab exam

Important commands and concepts

| Command / Concept               | Purpose                       |
| ------------------------------- | ----------------------------- |
| `sudo systemctl start jenkins`  | Starts Jenkins                |
| `sudo systemctl status jenkins` | Checks Jenkins status         |
| `localhost:8080`                | Opens Jenkins dashboard       |
| Git                             | Source code management        |
| Freestyle Project               | Creates a Jenkins job         |
| Poll SCM                        | Checks repository for changes |
| Build Now                       | Executes the build            |
| Console Output                  | Displays build logs           |

Remember: Continuous Integration (CI) means frequently integrating code changes into a shared repository and automatically building and testing them. Continuous Delivery/Deployment (CD) extends this process by preparing or automatically releasing the application.
