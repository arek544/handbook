# Install Docker Toolbox

`#docker` `#install` `#toolbox`

## What you get and how it works

Docker Toolbox is for older Mac and Windows systems that do not meet the requirements of [Docker Desktop for Mac](https://docs.docker.com/docker-for-mac/) and [Docker Desktop for Windows](https://docs.docker.com/docker-for-windows/). We recommend updating to the newer applications, if possible.

Docker Toolbox includes the following Docker tools:

- Docker CLI client for running Docker Engine to create images and containers
- Docker Machine so you can run Docker Engine commands from Windows terminals
- Docker Compose for running the `docker-compose` command
- Kitematic, the Docker GUI
- the Docker QuickStart shell preconfigured for a Docker command-line environment
- Oracle VM VirtualBox

Because the Docker Engine daemon uses Linux-specific kernel features, you can’t run Docker Engine natively on Windows. Instead, you must use the Docker Machine command, `docker-machine`, to create and attach to a small Linux VM on your machine. This VM hosts Docker Engine for you on your Windows system.

### Docker vs Docker Toolbox

One of the advantages of the newer [Docker Desktop for Windows](https://docs.docker.com/docker-for-windows/) solution is that it uses native virtualization and does not require VirtualBox to run Docker.

### Step 1: Check requirements

To run Docker, your machine must have a **64-bit** operating system running **Windows 7 or higher**. Additionally, you must make sure that **virtualization is enabled** on your machine.

### Step 2: Install Docker Toolbox

1. To download the latest version of Docker Toolbox, go to [Toolbox Releases](https://github.com/docker/toolbox/releases) and download the latest `.exe` file.
2. Install Docker Toolbox
3. Verify your installation
    
    Click the Docker QuickStart icon to launch a pre-configured Docker Toolbox terminal. If the system displays a **User Account Control** prompt to allow VirtualBox to make changes to your computer. Choose **Yes**.
    
    The terminal does several things to set up Docker Toolbox for you. When it is done, the terminal displays the `$` prompt.
    
    The terminal runs a special `bash` environment instead of the standard Windows command prompt. The `bash` environment is required by Docker.
    
4. Type the `docker run hello-world` command and press RETURN.
    
    The command does some work for you, if everything runs well, the command’s output looks like this:
    
    ```bash
    $ docker run hello-world
     Unable to find image 'hello-world:latest' locally
     Pulling repository hello-world
     91c95931e552: Download complete
     a8219747be10: Download complete
     Status: Downloaded newer image for hello-world:latest
     Hello from Docker.
     This message shows that your installation appears to be working correctly.
    
     To generate this message, Docker took the following steps:
      1. The Docker Engine CLI client contacted the Docker Engine daemon.
      2. The Docker Engine daemon pulled the "hello-world" image from the Docker Hub.
         (Assuming it was not already locally available.)
      3. The Docker Engine daemon created a new container from that image which runs the
         executable that produces the output you are currently reading.
      4. The Docker Engine daemon streamed that output to the Docker Engine CLI client, which sent it
         to your terminal.
    
     To try something more ambitious, you can run an Ubuntu container with:
      $ docker run -it ubuntu bash
    
     For more examples and ideas, visit:
      https://docs.docker.com/userguide/
    ```