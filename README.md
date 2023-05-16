# Microservice Architecture with Docker and K8

## What is a Microservice (MS)

- Microservices are a way of building software where an application is split into a set of small, independent, and loosely coupled services. 
- Each service performs a specific function and communicates with others through APIs or message queues. This architecture allows developers to work on individual services independently, making it faster and more efficient to build and deploy software. 
- It also provides greater flexibility, scalability, and resilience, as failures in one service do not affect the rest of the system. Microservices are a popular approach for building modern, cloud-based applications.

## What is the difference between 2-tier architecture and Miscroservices architecture

- In a 2-tier architecture, the application is divided into two layers: the presentation layer (for the user) and the data layer.
- Microservices architecture, on the other hand, breaks down the application into multiple independent services, each performing a specific function and communicating with each other through APIs or message queues.

## What is Containerisation?

- Containersation is a way of packaging software applications along with their dependencies into portable units called **containers**. 
- A container is a lightweight, standalone, and executable package that contains everything an application needs to run, including code, libraries, system tools, and runtime. 
- Containerisation provides a consistent and isolated environment for running applications, making it easier to deploy and scale them across different platforms and environments. It allows developers to package and ship applications as a single unit, without worrying about the underlying infrastructure or dependencies. Containers are widely used in modern software development and are a key component of cloud-native architectures.

### How does it differ from virtualisation?

- Containerisation is a lightweight form of virtualisation that virtualizes the operating system instead of the hardware. Containers run on top of a host OS and share the ***kernel*** with other containers on the same host. 
- Each container is isolated from the others and has its own set of resources, but it does not require a full OS. Containers are much lighter and faster than VMs, as they share resources with the host and require only the libraries and dependencies needed to run the application. This makes containerization a popular choice for cloud-native applications, where scalability and portability are important factors.

**Kernel** - Core component of an operating system that manages system resources and provides a bridge between applications and hardware.

## What is Docker?

![2023-05-15](https://github.com/janeteneto/Docker/assets/129942042/570f3eed-6d03-408b-89d2-394788ee2dad)


- Docker is a platform that allows developers to create, deploy, and run applications in containers. 
- With Docker, developers can build, test, and deploy applications faster and more efficiently, as containers can be easily distributed and scaled. Docker is widely used in modern software development and is an important tool for building cloud-native applications.

### Docker Container

- Once Docker is installed and running, open a Git Bash terminal on any directory:

1. Run `docker run -d -p 80:80 nginx`

2. Go to `http://localhost/` and nginx should be running

3. `docker rm (container id) -f` - removes container

4. `docker exec -it 607f81d7b0f3 sh` - executes container in linux subsystem

5. `alias docker="winpty docker"` - uses container in docker alias 

6. Cd into `/usr/share/nginx/html` and run command `pwd` to check if you're in the right file.

7. Run `apt update -y`

8. Run `apt-get install sudo`

9. Run `sudo apt install nano -y`

10. Run `sudo nano index.html`
- From this file, you can make changes to the html page on your local host.

### Build image and push to Docker Hub

1. On your local terminal, run `nano index.html` to create this file and add the following code:
````
<!DOCTYPE html>
<html>
<head>
<title>Janete's Page</title>
<style>
html { color-scheme: light dark; }
body { width: 35em; margin: 0 auto;
font-family: Tahoma, Verdana, Arial, sans-serif; }
</style>
</head>
<body>
<h1>Welcome to Janete's Profile page!</h1>
````
- Replace my name for your own
- This creates an html page with the above details

2. Copy the file to the previous container with the command:
````
docker cp index.html 607f81d7b0f3:/usr/share/nginx/html
````

3. Run `docker run -d -p 90:80 nginx` to have your index file on another container with port 90 using nginx's image.
- Now if you browse localhost on your browser you should see your profile, and on port 90 you should see nginx's welcome page. 

4. To create and name your image based on a cointainer run `docker commit (cointaner's name) (name image)`

5. Now login to your DockerHub on your terminal with command ``docker login` and enter your credentials

6. Run `docker tag nameofimage username/nameofimage:inserttag`
- For eg., mine looks like `docker tag janeteprofile janeteneto/janeteprofile:v1`

7.  Finally, to push to Dockerhub, run `docker push janeteneto/janeteprofile:v1`

### Docekrfile

1. On localhost, do `nano Dockerfile`

2. Add the following code:
````
FROM nginx
LABEL MAINTAINER=JANETE
COPY index.html /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
````

3. Make a small change to the `index.html` file to see if the following steps will be deployed correctly

4. Do `docker ps` and make sure to remove any containers running on port 80. Use the `docker rm (container id) -f` to force the removal

5. Run `docker build -t nginx:v1 .` - this will create an image using the Dcokerfile you just created.
- The `.` means that it will be created on the present directory

6. Run `docker run -d -p 90:80 janeteprofile/nginx:v1` then check if it reflected on localhosts:90

7. Run `docker tag nginx janeteneto/nginx:v1`

8. `Then push with command janeteneto/nginx:v1`

### Docekrfile 
On the same directory as app folder (do not cd into app):
1. Run `nano Dockerfile` and add the following code:

````
FROM node:16
LABEL MAINTAINER=JANETE
WORKDIR /app
COPY app/ .
EXPOSE 3000
RUN npm install
CMD ["npm", "start"]
````

2. Run `docker build -t app:v1`
3. `docker run -d -p 3000:3000 app:v1`
