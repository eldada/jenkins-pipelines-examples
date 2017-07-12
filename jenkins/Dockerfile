FROM jenkins:2.60.1

# Inspired by https://github.com/Logimethods/docker-jenkins
# This Jenkins image will be able to run docker commands

# Install Docker (as root)
USER root
RUN apt-get -qq update && \
    apt-get -qq -y install curl && \
    curl -sSL https://get.docker.com/ | sh

# Allow jenkins user to run docker
RUN usermod -a -G staff,docker jenkins

# Switch back to user jenkins
USER jenkins
