# Easy-peacy Jenkins
A fast and easy to configure dockerized Jenkins container with docker-compose, based on the [Official Jenkins Continuous Integration and Delivery server on Docker Hub](https://hub.docker.com/r/jenkins/jenkins).

<img src="https://jenkins.io/sites/default/files/jenkins_logo.png"/>

# Prerequisites
- [Docker](https://docs.docker.com/engine/install/)
- [docker-compose](https://docs.docker.com/compose/install/)
- a host machine running a compatible Linux distribution

Versions used for this build:
- Docker version 20.10.11, build dea9396
- docker-compose version 1.29.2, build 5becea4c

# Initial Configuration
In the supplied .env file, please configure the target directories for the bound volumes:
```
JENKINS_HOME=~/jenkins_home
JENKINS_WORKSPACE=~/jenkins_workspace
```
The default directory is in /root. Please change these environment variables to point to the absolute path that you want on your machine. For example:
```
JENKINS_HOME=/home/myusername/jenkins_home
JENKINS_WORKSPACE=/home/myusername/jenkins_workspace
```

There is also an optional port configuration:
```
MAIN_PORT=8080
CONTROLLER_PORT=50000
```
Please change these if these ports are already in use on your host machine.


# Usage
After forking/downloading, navigate to the root directory of the project and run this in a terminal (you will be asked for your password):
```
./dockerup.sh
```
This will spin up the Jenkins docker container and run the installation. You can safely close the terminal after the installation is complete.

To stop and completely remove the docker container:
```
./dockerdown.sh
```
This will remove the container and related network, and is not a destructive action. Data will only be lost if:
- the folders specified by the environment variables in the Initial Configuration are deleted
- the MAIN_PORT and CONTROLLER_PORTS are changed in between dockerup and dockerdown sequences (configuration errors)

# Additional Configuration
For additional customizations, you may edit these environment variables in the .env file:
```
DOCKER_IMAGE=jenkins/jenkins:lts-jdk11
CONTAINER_NAME=jenkins_lts
NETWORK_NAME=jenkins
VERSION=1
```
The "DOCKER_IMAGE" environment variable allows you to select any Jenkins image that is available on the [Official Jenkins Docker Hub page](https://hub.docker.com/r/jenkins/jenkins)

# Notes

## Permissions issues

### Docker commands permission denied

In case you get the following (or similar) error while running any of the scripts:
> Got permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Get "http://%2Fvar%2Frun%2Fdocker.sock/v1.24/containers/json": dial unix /var/run/docker.sock: connect: permission denied


Please make sure to add your username ($USER) to the docker group:
```
sudo usermod -G docker -a $USER
```
Then restart the docker service:
```
sudo service docker restart
```
Then logout/login for the changes to take effect.

### Shell scripts not working
In the rare event that the shells scripts do not work, please make them executable as follows:
```
sudo chmod +x dockerdown.sh
sudo chmod +x dockerup.sh
```

You should be able to run them as usual after this.

# Contact
Hope you enjoy this quick and easy dockerized Jenkins implementation. If you have any questions or suggestions on how to improve this code, feel free to contact me via email.