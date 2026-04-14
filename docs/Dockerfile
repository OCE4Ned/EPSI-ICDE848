FROM jenkins/jenkins:latest
USER jenkins
RUN jenkins-plugin-cli --plugins "docker-workflow json-path-api"
RUN jenkins-plugin-cli --plugins "git"
RUN jenkins-plugin-cli --plugins "ssh-slaves"