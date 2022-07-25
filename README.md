# BOOTSTRAP CSS + NGINX + DOCKER

Simple Nginx server docker container running a static Bootstrap template - [`startboostrap-heroic-features`](https://github.com/BlackrockDigital/startbootstrap-heroic-features)

## How to run

You will need podman on your machine.

Install Podman using Home-brew

Install podman with the following command: brew install podman
Create a machine in qemu (installed by home-brew) with the following command: podman machine init
Start the machine so it can be used, with the following command: podman machine start
Symlink docker for podman ln -s podman docker  (in /usr/local/bin e.g. cd /usr/local/bin; ln -s podman docker), so it's a true drop in replacement. Alternatively you may want to alias docker to podman alias docker=podman
Try running docker run hello-world to test or doing a docker pull <fully-qualified-image-name>
You might also want to look at https://podman.io/getting-started/installation#macos & https://www.redhat.com/sysadmin/podman-mac-machine-architecture & https://www.redhat.com/sysadmin/replace-docker-podman-mac-revisited

Note: Because podman runs in rootless mode by default, certain functions such as the use of certain ports, will be restricted when you switch to podman until you either modify the settings in podman or modify your files. This is not recommended as it will lessening security, but you can change to defaulting to using the podman in root after installing and initializing it by entering: podman system connection default podman-machine-default-root. If this does not work, you likely are only connected to the default rootless machine and need to add it using the instructions found below in the instructions for Mac users who are upgrading podman. The recommended solution is to run rootless.

View the connection list with podman system connection list
If there are more than the two default machines:
If there are machines other than podman-machine-default and podman-machine-default-root, remove them using podman system connection remove [name of machine you want to remove]
If one of the two default machines are missing:
Add one or both of the two default machines (podman-machine-default and podman-achine-default-root) using podman system connection add --identity [identity of the other machine] [whichever name is not in the list] [if you're adding root switch "core" to "root" and add "/user/1000" after "run", if you are adding default, do the opposite]
  
  

```bash

# podman setup
brew install podman
podman machine init  
podman system connection default podman-machine-default-root  ???
podman machine set --rootful
podman machine start
ln -s podman docker

# Build Image
docker build -t air-nscc-website .

# Run container
docker run -d -p 80:80 air-nscc-website

# Confirm container is running
docker container ls

# login to docker.io
docker login -u youerusename docker.io

# list docker images
docker images 

# add a tag
docker tag 79c9fadbe351 youerusename/air-nscc-website:v1

# push docker images to dockerio
docker push youerusename/air-nscc-website:v1

```
VERSION 20200725
Markus
