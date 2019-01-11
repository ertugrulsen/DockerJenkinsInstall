"# DockerJenkinsInstall" 

The Jenkins Continuous Integration and Delivery server available on Docker Hub.

This is a fully functional Jenkins server. https://jenkins.io/.

**docker run -p 8080:8080 -p 50000:50000 jenkins/jenkins:lts**
NOTE: read below the build executors part for the role of the 50000 port mapping.

This will store the workspace in /var/jenkins_home. All Jenkins data lives in there - including plugins and configuration. You will probably want to make that an explicit volume so you can manage it and attach to another container for upgrades :

**docker run -p 8080:8080 -p 50000:50000 -v jenkins_home:/var/jenkins_home jenkins/jenkins:lts**
this will automatically create a 'jenkins_home' docker volume on the host machine, that will survive the container stop/restart/deletion.

NOTE: Avoid using a bind mount from a folder on the host machine into /var/jenkins_home, as this might result in file permission issues (the user used inside the container might not have rights to the folder on the host machine). If you really need to bind mount jenkins_home, ensure that the directory on the host is accessible by the jenkins user inside the container (jenkins user - uid 1000) or use -u some_other_user parameter with docker run.

docker run -d -v jenkins_home:/var/jenkins_home -p 8080:8080 -p 50000:50000 jenkins/jenkins:lts
this will run Jenkins in detached mode with port forwarding and volume added. You can access logs with command 'docker logs CONTAINER_ID' in order to check first login token. ID of container will be returned from output of command above.

**docker pull Jenkins**

**docker run --name jenkins -d -v /Users/jenkins:/var/jenkins_home -p 8080:8080 -p 50000:50000 jenkins:latest**

**docker ps -a**

