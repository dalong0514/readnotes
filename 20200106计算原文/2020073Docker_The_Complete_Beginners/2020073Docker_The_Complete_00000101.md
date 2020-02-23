# 01 Getting Started with Docker

Docker is basically an open source and anyone can subsidize to Docker and expand it to your own needs. If you need additional features and these are not available, you can add them in the Docker.

This tool is good for system administrators and developers. It is an important part of DevOps (developers and operations) tool chains. Developers can pay attention on the writing code without thinking about system that it may ultimately be run on.

It enables them to get one head start with the use of thousands of predesigned programs to run in the Docker container. The operations staff can reduce the requirements of systems and increase their flexibility and productivity. It is a good way to reduce your overhead and footprint.

### Getting Started with Docker

There are some helpful resources to get started with Docker to maintain your workflow. You will get one web-based tutorial along with one command-line simulator. It will help you to try basic commands of Docker and understand it’s working.

### Security and Docker

Docker increase the security of all applications running in the shared environment, but the containers may not be an alternate of security measures. You have to understand the security features of Docker to keep your containers secure. You will find about the security of Docker in last chapter. Basically Docker has three important elements, such as: 1) Docker. 2) Images Docker. 3) Containers Dockerfiles.

As one project, Docker offers a complete set of high-quality tools to transfer everything to make one application across machines and systems, physical or virtual, and brings loads of benefits with it.

Docker achieves full-bodied application and process and reserve containment via Containers of Linux, such as Kernel features and namespaces. The further capabilities may come from different components and parts of one project that extract the intricacy of working along with the low-level tools and APIs of Linux. These are used for the application and system management with regards to the secure containing procedures.

### Main Parts of Docker Project

Project of Docker consists of different main elements and parts that all are designed on the top of existing functionality, frameworks and libraries offered by Linux Kernel or any third party, such as aufs, mapper or LXC.

### Basic Parts of Docker

Daemon of Docker is used to manage LXC (docker) containers on its current host. 

CLI of docker is used to communicate and give command to docker daemon. 

Image index of docker is a private or public repository for the images of docker.

### Elements of Docker

Containers of docker are directors with everything about your application. 

Images of docker are snapshots of base OS (for instance, Ubuntu) or containers. 

Dockerfiles are scripts to automate the building procedure of images.

These elements are utilized by these applications making the project of the docker:

### Docker Containers

This whole method of porting submissions with the use of docker depends on the container’s shipment. These containers are directories that may pack (tar-archive) like others.

It can share and run crossways various platforms (hosts) and machines. You have to dependent on the host to run these containers. You have to install docker for this procedure. Containers are obtained through LXC (Linux Containers).

### Linux Containers (LXC)

You can define these containers as an amalgamation of different Kernel-level features. It enables you to manage your applications and have their own environment. With the use of certain features, such as chroots, namespaces, SELinux and cgroups profiles, the LXC may contain application procedure and help with the management through restricted resources.

It may not allow you to reach beyond your file-system and restrict access to the namespace of parent. With containers, the docker makes it easy to use LXC and brings much more benefits along.

### Docker Containers

The containers of docker have various main features and these features enable you to get the advantage of: 1) Isolating procedure. 2) Application portability. 3) Prevent any assuaging with the external source. 4) Management of resource consumption.

As compared to traditional virtual-machines, they require fewer resources for the deployment of isolated applications.

You are not allowed for: 1) Messing with remaining procedures. 2) Dependency hell may be caused. 3) May not work on the different system. 4) You may be vulnerable to abuse and attacks to all resources of the system.

Being depending and based on the LXC, makes one technical aspect and these containers are similar to directory, but one formatted and shaped one. This may increase the portability and gradually construct containers.

Every container may layer like one onion and every action may be taken within one container comprises of putting a separate block that actually translated to the simple change within your file system on the top of previous one. Various configurations and tools make this set-up effective in a melodious manner altogether (e.g. file-system).

This method will make containers extremely beneficial for you because you can easily create and launch new images and containers. These are kept lightweight because of layered and gradual procedure.

Everything required a file-system and take performing roll-backs and snapshots in particular times. You can get the advantage of VCS (version-control systems). Docker containers initiate from the docker image that make the base of various other layers and applications.

### Docker Images

These images establish the foundation of docker container and it is a point when everything just starts to form. These are similar to the default disk images of operating system that are utilized to run different applications on desktop computers and servers.

These images will help you to get the advantage of seamless movability across systems. You can make consistent, dependable and solid base with each and everything. It is required to run all applications.

With self-contained options, the risks of system-level modifications or updates may be eliminated and the container turns out to be immune for the external exposure. This immune is important to prevent the hell dependency.

Some extra layers of applications and tools are added on the top of this base and the new images may be designed with the help of committed changes. A new container may be created from saved things and images to continue this procedure. The file system (unionfile-system) brings every layer together as one single entity and you may work with one container.

These foundation images may explicitly state the working with CLI docker to directly form one new container and they may be specified in one Dockerfile to automate image building.

### Dockerfiles

These are scripts with a series of consecutive instructions, commands and directions that can be executed to make one new docker image. Every executed command is translated to one new layer of onion and makes the end product.

They can replace the procedure of undertaking everything repeatedly and manually. A Dockerfile may finish its execution and you may make one image to start one new container.