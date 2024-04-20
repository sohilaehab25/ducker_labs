# ducker_labs
taskd of ducker to iti_9mounth_os_track

# ITI - Docker Lab 🐋

## Task 1: Working with Docker Hello-world Image
### Objective
Learn how to run a container using the hello-world image and manage containers and images.

### Steps
#### 1. Run a Container with hello-world Image
docker run hello-world
docker pull hello-world
```
#### 2. Check Container Status and Explain
docker ps -a
The container status is "Exited (0)" ->  The reason for this status is that the hello-world container is a very simple container that is designed to just print a message ("Hello from Docker!") to confirm that your Docker installation is working correctly. After printing this message, the container completes its task and exits 
```
#### 3. Start the Stopped Container
docker start hello-world
```
#### 4. Remove the Container
docker rm trusting_northcutt
```
#### 5. Remove the Image
docker rmi hello-world
```
---

## Task 2: Running Container with Ubuntu Image
### Objective
Run an Ubuntu container in interactive mode, create a file inside it, and manage containers.

### Steps
#### 1. Run Ubuntu Container in Interactive Mode
docker pull ubuntu
docker run -it ubuntu
```
#### 2. Create a File inside the Container
touch hello-docker
```
#### 3. Stop and Remove the Container
exit
docker stop zealous_roentgen
docker rm zealous_roentgen
```
#### 4. Check File Status
removed
```
#### 5. What happened to hello-docker file?
Docker removes the container along with all its associated files and changes, including the "hello-docker" file
```
#### 6. Remove All Stopped Containers

docker rm -f $(docker ps -aq)
```
#### 7. Bonus: Remove All Containers in One Command
docker container prune
```

---
## Task 3: Creating a Custom Nginx Docker Image
### Objective
Create a custom Docker image using Nginx and a local HTML file.

### Steps
#### 1. Create a Local HTML File
index.html <h1>hello world</h1>
```
#### 2. Write Dockerfile and Copy the HTML file to the Docker Image
vi  dockerfile :
           FROM nginx:alpine
           COPY index.html /usr/share/nginx/html/index.html
           EXPOSE 80
```
#### 3. Run Container with New Image
docker build -t nginx-custom .
```

#### 4. Test the Container, open your browser and navigate to http://localhost:8088 to check if everything is okay
docker run -d -p 8080:80 nginx-custom
docker ps -a
(add port 8080 and get link and will work )
```
