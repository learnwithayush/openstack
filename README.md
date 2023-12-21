# openstack
ci-cd automatin using jenkins, terrafom and openstack
# openstack
ci-cd automatin using jenkins, terrafom and openstack


# Docker-Jenkins
$ docker network create jenkins

# build
Build a new docker image from this Dockerfile, and assign the image a meaningful name, such as "myjenkins-blueocean:2.426.2-1":

$ docker build -t myjenkins-blueocean:2.426.2-1 .

# run 
$ docker run \
  --name jenkins-blueocean \
  --restart=on-failure \
  --detach \
  --network jenkins \
  --env DOCKER_HOST=tcp://docker:2376 \
  --env DOCKER_CERT_PATH=/certs/client \
  --env DOCKER_TLS_VERIFY=1 \
  --publish 8080:8080 \
  --publish 50000:50000 \
  --volume jenkins-data:/var/jenkins_home \
  --volume jenkins-docker-certs:/certs/client:ro \
  myjenkins-blueocean:2.426.2-1


	( Optional ) Specifies the Docker container name for this instance of the Docker image.
Always restart the container if it stops. If it is manually stopped, it is restarted only when Docker daemon restarts or the container itself is manually restarted.
( Optional ) Runs the current container in the background, known as "detached" mode, and outputs the container ID. If you do not specify this option, then the running Docker log for this container is displayed in the terminal window.
Connects this container to the jenkins network previously defined. The Docker daemon is now available to this Jenkins container through the hostname docker.
Specifies the environment variables used by docker, docker-compose, and other Docker tools to connect to the Docker daemon from the previous step.
Maps, or publishes, port 8080 of the current container to port 8080 on the host machine. The first number represents the port on the host, while the last represents the container’s port. For example, to access Jenkins on your host machine through port 49000, enter -p 49000:8080 for this option.
( Optional ) Maps port 50000 of the current container to port 50000 on the host machine. This is only necessary if you have set up one or more inbound Jenkins agents on other machines, which in turn interact with your jenkins-blueocean container, known as the Jenkins "controller". Inbound Jenkins agents communicate with the Jenkins controller through TCP port 50000 by default. You can change this port number on your Jenkins controller through the Security page. For example, if you update the TCP port for inbound Jenkins agents of your Jenkins controller to 51000, you need to re-run Jenkins via the docker run …​ command. Specify the "publish" option as follows: the first value is the port number on the machine hosting the Jenkins controller, and the last value matches the changed value on the Jenkins controller, for example,--publish 52000:51000. Inbound Jenkins agents communicate with the Jenkins controller on that port (52000 in this example). Note that WebSocket agents do not need this configuration.
Maps the /var/jenkins_home directory in the container to the Docker volume with the name jenkins-data. Instead of mapping the /var/jenkins_home directory to a Docker volume, you can also map this directory to one on your machine’s local file system. For example, specify the option --volume $HOME/jenkins:/var/jenkins_home to map the container’s /var/jenkins_home directory to the jenkins subdirectory within the $HOME directory on your local machine — typically /Users/<your-username>/jenkins or /home/<your-username>/jenkins. NOTE: If you change the source volume or directory for this, the volume from the docker:dind container above needs to be updated to match this.
Maps the /certs/client directory to the previously created jenkins-docker-certs volume. The client TLS certificates required to connect to the Docker daemon are now available in the path specified by the DOCKER_CERT_PATH environment variable.
The name of the Docker image, which you built in the previous step.


on faliure 
docker run --name jenkins-blueocean --restart=on-failure --detach \
  --network jenkins --env DOCKER_HOST=tcp://docker:2376 \
  --env DOCKER_CERT_PATH=/certs/client --env DOCKER_TLS_VERIFY=1 \
  --publish 8080:8080 --publish 50000:50000 \
  --volume jenkins-data:/var/jenkins_home \
  --volume jenkins-docker-certs:/certs/client:ro \
  myjenkins-blueocean:2.426.2-1

  # post installation 
  http://localhost:8080

  got to 
  $sudo cat /var/lib/jenkins/secrets/initialAdminPassword
   for docker official image 
   $ sudo docker exec ${CONTAINER_ID or CONTAINER_NAME} cat /var/jenkins_home/secrets/initialAdminPassword

   
