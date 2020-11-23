FROM jenkins/jenkins:lts
 # Switching to root user to install .NET Core SDK
USER root

# Show the distro information during compilation!
RUN uname -a && cat /etc/*release

# Based on instructions at https://docs.microsoft.com/en-us/dotnet/core/install/linux-debian#debian-9-
# Installing with APT can be done with a few commands. Before you install .NET SDK, run the following commands 
# to add the Microsoft package signing key to your list of trusted keys and add the package repository.
RUN wget -O - https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.asc.gpg && \
    mv microsoft.asc.gpg /etc/apt/trusted.gpg.d/ && \
    wget https://packages.microsoft.com/config/debian/9/prod.list && \
    mv prod.list /etc/apt/sources.list.d/microsoft-prod.list && \
    chown root:root /etc/apt/trusted.gpg.d/microsoft.asc.gpg && \
    chown root:root /etc/apt/sources.list.d/microsoft-prod.list


# Install the .Net Core SDK, set the path, and show the version of core installed.
RUN apt-get update && \
    apt-get install apt-transport-https && \
    apt-get update && \
    apt-get install -y dotnet-sdk-3.1 && \
    export PATH=$PATH:$HOME/dotnet && \
    dotnet --version

# Switching back to the jenkins user.
USER jenkins