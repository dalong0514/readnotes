# 02 Tips to Install Docker for Mac

If you want to install docker, you have to check your system requirements. You can create a docker machine on Mac and copy your images and container from default machine to new docker for HyperKit VM. For Mac, you have to check these requirements:

Your Mac should have latest model with intel hardware, MMU (memory management virtualization and EPT (extended-page tablets).

Operating System X 10.10.3 Yosemite or latest 

Almost 4GB RAM 

VirtualBox proceeding to the version 4.3.30 should not be installed and it is incompatible with the mac for docker.

Note: If your system doesn’t fulfill these requirements, you should install Toolbox of Docker that uses Virtual Box of Oracle in its place of HyperKit. The installation includes Docker CLI, Docker Enginer, Docker Machine and Docker Compose.

### Step 01: Run and Install Docker for Mac

Double-click the Docker.dmg the Applications folder.

Now, you have to permit Docker.app using password of your system throughout the installation procedure. You will need privileged access to install the components of networking and links to the apps of Docker.

Double-click the Docker.app to initiate Docker.

You will see a whale in the upper status bar that indicates the running status of docker, and you can easily access docker from one terminal.

After installing this app, you can get one success message and subsequent suggestions and

one link for documentation. You have to click the whale ( terminate this popup.

You have to tap the whale () and get some Preferences, and several other choices.

You have to choose “About Docker” to authenticate that your system has the latest version.

Well done! The latest Docker is running for Mac on your system.

### Step 02: Focus on the Available Versions of the Docker Engine, Machine and Compose

You have to run these important commands in your docker to check the version, such as docker, docker-compose & docker-machine. Make sure these all are compatible and updated to the Docker.app.

```
docker --version
docker-compose --version
docker-machine --version
```

Note: This example will help you to understand docker installation. Your own output can be different with a different version.

### Step 03: Run Examples and Explore Applications

You can open the terminal of command-line and run a few docker commands to authenticate that the docker is working as per your expectations. There are some commands to try, such as docker version is good to check the latest version, and the docker ps along with docker-run-hello-world is good to authenticate that docker is successfully running. If you want some adventure, you can start with web server dockerized.

    docker run -d -p 80:80 --name webserver nginx

If you are unable to find a local image, the docker can pull it for your assistance from a docker hub. In your web browser, you can use http://localhost/ to get your home page. (Meanwhile you itemized the default port of HTTP and it is not essential to affix :80 at the final part of your URL.)

Note: Initial beta issues utilized docker as hostname to create the URL. The ports may be exposed on the IP addresses (private) of VM and accelerated to the local host without host name. You can see release for Beta 09.

You can run docker ps although the web serve may run to check the details of your web server container.

Remove or Stop Images and Containers. The webserver nginx will endure to run the container on the port until you remove or stop the container. Anyone who wants to stop webserver can type docker-stop-webserver and initiate it once again with the help of docker-start-webserver. 

If you want to remove and stop your running container with one command, you can write docker-rm -f-webserver. This may remove the container, but it is not good to remove nginx image. If you want to list some local images, you can use docker images.

If you want to keep a few images, there is no need to drag them once again from the hub of docker. You can remove one image as long as you don’t need it, you can use docker-rmi \<imageID>|\<imageName> for this procedure. For instance, docker-rmi-nginx can be the right command for you.

### Preferences

You can select —> preferences available in your menu bar. It will help you to set the runtime options.

General. Docker is available to set for your Mac to start it automatically after your log in. You have to uncheck the option of autostart login option to avoid opening of docker session with the start of computer.

Docker is all set to check the updates and you will get notification about available updates. If the updates are found, you can click “OK” to install and accept updates. You can also cancel them to use your current version. You can also disable updates by selecting and -> check for updates.

You can exclude the VM from the backups of your Time Machine and prevent your time Machine from docker’s backing up for the virtual machine.

The CUPs, by default, your docker for the Mac is all set to utilize two processors. It is good to increase the processing power of your app by setting it to lower or higher number to have it with docker for the use of Mac with limited computing resources.

Memory: The Docker (by default) for Mac can use 2GB runtime-memory. It is allotted from the entire accessible memory on the Mac. It is possible to increase the RAM on your app to get the advantage of quicker performance and adjust this number to higher number, such as 3 or lower, such as 1. You can adjust the memory usage of your docker.

Advanced

Addition of registries: It can be used as a substitute to use the hub of docker to store the private and public images or the trusted registry of docker. It is easy to use docker to adjust your own apprehensive registry. Users can add URLs for insecure registry mirrors and registries to host all your images.

HTTP Settings for Proxy: Docker with your mach can detect HTTPS and HTTP automatically propagate and proxy settings to docker and your containers. For instance, if you want to set proxy setting for you, you can visit http://proxy.example.com and the docker may use this proxy to pull containers.

Share Files

If you want to share files, you have to select directories on the Mac to share them with containers. You can click “+” to add one directory and navigate the directory that you are interested to add.

You have to hit apply and restart the available directories on the container with the use of bind mount of docker “-v” feature.

You may face some limitations on your directories and these may be shared:

You can’t make a subdirectory of a shared directory. They may not previously exist in docker.

Privacy

It is easy to set docker for your mac to auto-send crash report, usage data and diagnostics. These details prove helpful for docker to bring improvements in the application and get maximum context to troubleshoot problems.

You can uncheck any option to prevent auto-sending of any data. The docker can prompt for extra information in various cases and you can enable auto-send as well.

It is easy to disable and enable the auto-reporting adjustments with just one click on the popup for information, as you start your docker.

Reset or Uninstall

You can select —> options from your menu bar and hit Uninstall or Reset on the dialog of Preferences.

Uninstall: You can select this choice to remove this docker from your system and Mac.

Factory defaults (Reset): This option will help you to reset all your options on the docker. It will take to the initial level as you first time install docker. You can uninstall docker for your mac by using one command-line terminal:

Bash completion Installation

If you want to use bash completion, including “homebrew-bash-completion on your Mac” and bash completion script for the docker compose, docker machine and docker is easy to find in the docker.app and you can get it in resources or contents folder.

You can activate the completion of bash and these files should be symlinked or copied to the bash_completion.d directory. For instance, you can use Homebrew:

