# Installing Nginx on docker + port mapping

## Objective

The objective of this tutorial is to download the Nginx image onto Docker and run that container plus bind the port so we can view within a web browser using Linode's Cloud hosting platform.

### Skills Learned

By completing this lab, I will gain hands-on experience with Docker installation procedures, container creation, donwloading images and port mapping enabling me to incorporate containerization technology into my development workflow effectively.

### Tools Used

- Linode - Cloud Hosting Platform
- Solar Putty - To connect to the platform
- Docker - To create the containers
- Nginx - Web Server

## What is Docker

Docker is an open-source platform that automates the deployment, scaling, and management of applications inside containers. Containers are lightweight, portable, and self-sufficient units that encapsulate the application code, runtime, system tools, libraries, and settings required to run the application. Docker provides a standardized way to package and distribute applications, allowing developers to build, ship, and run their applications seamlessly across different environments, from development to production. With Docker, developers can create isolated environments for their applications, ensuring consistency and reliability across various infrastructure platforms, whether it's on-premises, in the cloud, or hybrid environments.

## Step 1 - Creating and Installing Docker

To start will will create our Linode

![image](https://github.com/Matt4llan/Docker-Basic/assets/156334555/9a016270-3968-42ec-9f34-f2f1a2f36eb2)

Then select Docker from the marketplace

![image](https://github.com/Matt4llan/Docker-Basic/assets/156334555/1fec71bf-415d-4238-b222-4e5f194ec30c)

Image:  Ubuntu 22.04 LTS for stability and long term support
Region: London
Server: 2GB RAM, 1 CPU, 50GB Storage, 2TB Transfer
Label: docker-matt-basic
Setting a root password and clicking create.

![image](https://github.com/Matt4llan/Docker-Basic/assets/156334555/0a26caaf-72a2-47ea-a4e1-64b18e4a7afd)

## Step 2 - Connecting to the new image

![image](https://github.com/Matt4llan/Docker-Basic/assets/156334555/0fec12ea-e300-4746-8089-91107ca7e1d4)

## Step 3 - installing Docker
```
snap install docker
```

![image](https://github.com/Matt4llan/Docker-Basic/assets/156334555/e7349685-9bca-49c1-8276-88f5f3615566)

## Step 4 - Downloading the Nginx Image

I'm going to use the following commands to download Nginx
```
docker pull nginx:latest
```

- docker pull nginx:latest | This command downloads the latest Nginx image from Docker Hub to your local machine, making it available for use in creating containers.
- (note running just 'docker pull nginx' command will download the latest version, the ':latest' is a tag and is more used for a specific version of Nginx eg ':stable-perl'
 
![image](https://github.com/Matt4llan/docker-nginx/assets/156334555/fd688004-3de7-441a-84ea-661510f3287b)

![image](https://github.com/Matt4llan/docker-nginx/assets/156334555/8e59e27b-fe5f-4e7d-93b8-37aa8522fab5)


## Step 5 - Run the Nginx Container

I'm going to use the following commands to run the Nginx docker container
```
docker run -d nginx
```

- docker run -d nginx | This command creates a new container using the Nginx image. If a name has not been specified using  '--name' Docker will give it a random name and run in the background.
  - -d | Detached mode, which means the container runs in the background
  - nginx | Specifies the image to use for creating the container

![image](https://github.com/Matt4llan/docker-nginx/assets/156334555/cb498b7c-fcaf-4e69-8015-de8bbe361eb4)


## Step 5 - Testing on a web browser

Jumping into a web browser we need the server IP address and the tcp port number 80 and hit enter.

![image](https://github.com/Matt4llan/docker-nginx/assets/156334555/0f75c377-deed-45f6-ab9b-e996585475b6)

Nothing is available on this port, so i need to tell docker to bind port 80 to port 80 allowing me to access what ever is in the Docker container in this case Nginx.

## Step 6 - Port Binding

I'm going to use the following commands to stop the Nginx docker container and create a new Nginx container with the port

```
docker stop 66e8c7a9ce7b
docker run -d -p 80:80 nginx
```

- docker run -d -p 80:80 nginx | This command creates a new container using the Nginx image. If a name has not been specified using  '--name' Docker will give it a random name and run in the background.
  - -d | Detached mode, which means the container runs in the background
  - -p | This command is used to publish a container's port to the host
  - 80:80 | This command means that port 80 on the host machine is mapped to port 80 on the Docker container
  - nginx | Specifies the image to use for creating the container

![image](https://github.com/Matt4llan/docker-nginx/assets/156334555/6b596aeb-6b1d-46be-84af-eaa73378a734)
![image](https://github.com/Matt4llan/docker-nginx/assets/156334555/7244d8c4-128b-49a7-8ffb-6dda935b7188)


## Step 7 - Testing on a web browser

Jumping into a web browser we need the server IP address and the tcp port number 80 and hit enter.

![image](https://github.com/Matt4llan/docker-nginx/assets/156334555/16342435-309d-4688-a9cf-e08690e855a3)
