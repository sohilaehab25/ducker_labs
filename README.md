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







# ITI - Docker Lab2 🐋

## Task 1:
Run a container using nginx image, and mount a directory from your host into the 
Docker container. example: /home/samy/nginx:/home/nginx (bind mount)
```bash

##Steps

Create Bind Mount Directory
mkdir bindMount_dir
cd bindMount_dir
Run a container using nginx image
docker run -d --name bindMount_dir -v /root/bindMount_dir:/user/share/nginx/html nginx
docker exec -it bindMount_dir bash
Echo any content to show when curl ip-address
cd /user/share/nginx/html
echo "Hello from Bind Mount Nginx" > index.html
exit
docker inspect -f '{{.NetworkSettings.IPAddress}}' bindMount_dir    ->172.17.0.2
curl 172.17.0.2



## Task 2:
### Steps
#### 1. Create 2 docker network (net-1 & net-2)
```bash

docker network create network_1
docker network create network_2


#### 2. Run 2 new containers using nginx:alpine image, and attach the net-1 to them
```bash

docker run -d --name nginx_net1 --net network_1 nginx:alpine
docker run -d --name nginx_net2 --network network_1 nginx:alpine

#### 3.  Run another 1 new containers using nginx:alpine image, and attach the net-2 to them
```bash


docker run -d --name nginx_net3 --net network_2 nginx:alpine

#### 4. Inspect the 3 containers to know their IPs and write them aside
```bash


docker inspect -f '{{.NetworkSettings.Networks.network_1.IPAddress}}' nginx_net1
172.18.0.2

docker inspect -f '{{.NetworkSettings.Networks.network_1.IPAddress}}' nginx_net2
172.18.0.3

docker inspect -f '{{.NetworkSettings.Networks.network_2.IPAddress}}' nginx_net3
172.20.0.2

#### 5. Enter a container in the net-1 network and try to ping a container in the net-2 
network (What do you notice?)
```bash
docker exec -it nginx_net1 sh 
Use ping or curl
ping 172.20.0.2
ping fails, because the two containers exist in different networks so we can see any response in terminal.

#### 6. Enter a container in the net-1 network and try to ping the other container in the 
same network (What do you notice?)
```bash

docker exec -it nginx_net1 sh 
curl 172.18.0.2
ping 172.18.0.3
ping successful and return response, because the two containers exist in the same network.

```
---
## Task 3: Explain the difference between Docker volumes and Bind Mount.
```bash
Docker Volumes

Volumes are stored within the Docker environment, typically in a directory on the host filesystem, but the location is managed by Docker and not directly accessible or configurable by the user.

Docker Bind Mounts

Bind mounts give you more control over where the data is stored and how it's accessed because you can specify any path on the host machine.
```
















