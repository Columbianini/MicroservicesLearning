# TODO
- [learn more on docker](https://learn.microsoft.com/en-us/training/modules/intro-to-docker-containers/)


# What are microservices?
- In a **microservices architecture**, a large application is split up into a set of smaller services. Each service runs in its own process and communicates with other processes by using protocols like HTTP/HTTPS, WebSocket, or Advanced Message Queuing Protocol (AMQP).
- **Containerization** is an approach to software development in which an application or service, its dependencies, and its configuration (abstracted as deployment manifest files) are packaged together as a container image
- **Docker** is an open-source platform that you can use to automate the deployment of applications as portable, self-sufficient containers that can run in the cloud or on-premises.
- **service vs application**: Services are used by applications; applications are used by users. Services provide specific capabilities to applications while also providing a GUI, if needed, to manage said capabilities.
- **Docker image** is a static representation of the app or service and its configuration and dependencies. The image, when it runs, becomes the container. The container is the in-memory instance of an image. Image is immutable and when you need to change, just create a new image
- **Docker file** is a text file that is written in minimal script language and contains instructions on how to build a docker image
    - You can customize an image by starting a container with a [base image](## "e.g. mcr.microsoft.com/dotnet/aspnet"), and then make changes to it. Changes usually involve activities like copying files into the container from the local file system and running various tools and utilities to compile code.

# Microsoft Orchestra
- **orchestra**: tools that are used to manage the hosts (i.e. server/vm/pc) on which containers(i.e. instance of Docker image (i.e. unit of deployment for one specific service) ) run.
- Kubernetes is one such orchestrator
- For example, you might find during specific times of the day you need to scale up the number of container instances that handle caching, or you might have an update to the container instance that checks merchandise inventory.
    
# Deploy a .NET microservice to Kubernetes
## What are orchestrators?
- **Container Management** is the process of organizing, adding, removing, or updating a significant number of containers.
- For example, the orchestrator can dynamically respond to changes in the environment to **increase or decrease** the deployed instances of the managed app. It can also ensure all deployed container instances get **updated** if a new version of a service is released.
## Exercise - Push a microservice image to Docker Hub
- **Docker hub** could upload Docker images. **Kubernetes** could use Docker hub to create Docker images
- You first create Docker images
    - write docker-compose.yml and DockerFile (e.g. DockerfileProducts) 
    - docker compose build (then you could check the container by *docker compose up*)
- You second pushed the Docker images to Docker Hub to make the images available to the Kubernetes instance to download
    - docker login -u [your [Docker login](https://hub.docker.com/settings/general) id] - p [your Docker login passwork]
    - docker tag storeimage [YOUR DOCKER USER NAME]/[Docker image name, defined in docker-compose.yml above] 
    - docker push [YOUR DOCKER USER NAME]/[Docker image name, defined in docker-compose.yml above]
## Exercise - Deploy a microservice container to Kubernetes
- You third [install  kubectl tool and the k3d Kubernetes implementation](https://learn.microsoft.com/en-us/training/modules/dotnet-deploy-microservices-kubernetes/4-exercise-deploy-to-kubernetes)
- You fourth create deployment file e.g. frontend-deploy.yml, and then test by running it 
    - kubectl apply -f frontend-deploy.yml
    - kubectl get pods
## Exercise - Scale a container instance in Kubernetes
- You can then scale up/down the pods with name = deployment/{containers.name}
    - kubectl scale --replicas=5 deployment/productsbackend
    - kubectl scale --replicas=1 deployment/productsbackend
## Exercise - Prove microservice resilience in Kubernetes
- Kubernetes ensures the system state matches what is defined in the configuration files, regardless of the circumstances.




