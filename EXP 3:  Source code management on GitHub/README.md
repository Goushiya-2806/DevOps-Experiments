
# EXPERIMENT – 3

TITLE: Practice Source Code Management on GitHub

AIM:

To practice source code management using Git and GitHub by uploading the Event Registration Microservices project and performing version control operations.

SOFTWARE REQUIREMENTS:

1. Git
2. GitHub Account
3. Eclipse IDE
4. Spring Boot
5. Command Prompt / Git Bash

PROCEDURE:

Step 1: Create GitHub Repository

1. Login to [https://github.com](https://github.com?utm_source=chatgpt.com).
2. Click on New Repository.
3. Enter repository name: `event-registration-microservices`.
4. Select Public.
5. Click Create Repository.

Step 2: Prepare Project Folder

Create a parent folder named `EventRegistrationMicroservices` and place both projects inside it.

- event-service
- registration-service

Step 3: Initialize Git Repository

Open Git Bash inside the parent folder and execute:

```
git init
git status
```

Step 4: Create .gitignore File

```
touch .gitignore
```

Add the following content:

```
target/
.classpath
.project
.settings/
bin/
*.log
```

Step 5: Add and Commit Files

```
git add .
git status
git commit -m "Initial commit"
```

Step 6: Connect to GitHub

```
git branch -M main
git remote add origin https://github.com/Anil4799/event-registration-microservices.git
git push -u origin main
```

Step 7: Create a New Branch

```
git checkout -b event-update
```

Step 8: Modify Event Service

Open `EventController.java` and change the event name from Python Workshop to Advanced Python Workshop.

Step 9: Commit and Push Changes

```
git status
git diff
git add .
git commit -m "Updated event name"
git push -u origin event-update
```

Step 10: Merge Changes into Main

```
git checkout main
git merge event-update
git push origin main
```

Step 11: Update Registration Service

Open `RegistrationController.java` and modify the status message to:

`Event Registration Service is running successfully`

Execute:

```
git checkout -b registration-update
git add .
git commit -m "Updated registration service"
git push -u origin registration-update
```

Merge into main:

```
git checkout main
git merge registration-update
git push origin main
```

RESULT:

Thus, source code management was successfully practiced using Git and GitHub. The Event Registration Microservices project was uploaded, modified, committed, pushed, and merged using different Git branches.
