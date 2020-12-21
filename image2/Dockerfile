FROM jenkins/jenkins:lts
 # Switching to root user to install .NET Core SDK
USER root

# Show the distro information during compilation!
RUN uname -a && cat /etc/*release

# Install docker
RUN apt-get update -qq \
    && apt-get install -qqy apt-transport-https ca-certificates curl gnupg2 software-properties-common 
RUN curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add -
RUN add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/debian \
   $(lsb_release -cs) \
   stable"
RUN apt-get update  -qq \
    && apt-get install docker-ce docker-ce-cli containerd.io -y
RUN usermod -aG docker jenkins    

# Switching back to the jenkins user.
USER jenkins