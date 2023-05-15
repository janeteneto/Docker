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
