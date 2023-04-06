FROM jenkins/jenkins:2.397-jdk11

USER root

# Instalar Docker CLI
RUN apt-get update && \
    apt-get -y install apt-transport-https ca-certificates curl gnupg-agent software-properties-common 

RUN curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add -q - && \
    add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable" && \
    apt-get update && \
    apt-get -y install docker-ce-cli

RUN groupadd docker && usermod -aG docker jenkins

# Instalación de plugins
COPY plugins_extra.txt /usr/share/jenkins/ref/plugins_extra.txt
ENV JENKINS_HOME /var/jenkins_home

ARG JAVA_OPTS
ENV JAVA_OPTS "-Djenkins.install.runSetupWizard=false ${JAVA_OPTS:-}"

COPY jenkins-plugin-manager-2.12.11.jar jenkins-plugin-cli.jar
RUN java -jar jenkins-plugin-cli.jar --plugin-file /usr/share/jenkins/ref/plugins_extra.txt --verbose


