```bash
###Create the virtual machines

gcloud compute instances create master worker-1 worker-2 --create-disk=auto-delete=yes,boot=yes,image=projects/ubuntu-os-cloud/global/images/ubuntu-1804-bionic-v20211115 --zone us-central1-a --machine-type=e2-medium

```

# To Create a User in Ubuntu follow the below steps: (Both master and worker)

```bash

$ adduser username
#Example
adduser chandu

#Add the new user to the sudo group 
usermod -aG sudo username
#Example
usermod -aG sudo chandu

Switch to newly created user:
su - username

#How to Enable SSH Password Authentication
#To enable SSH password authentication, you must SSH in as root to edit this file:
/etc/ssh/sshd_config

PasswordAuthentication yes

sudo service ssh restart

```

# Install Docker on all nodes (Both master and worker)

https://docs.docker.com/engine/install/ubuntu/

```bash

# Set up the repository
sudo apt-get update
sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg \
    lsb-release -y


# Add Docker’s official GPG key:
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

# Use the following command to set up the repository:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

# Install Docker Engine
sudo apt-get update


# To install the latest version, run:
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin -y


# To install specific version , do refer documentation

sudo apt-mark hold docker-ce
sudo usermod -aG docker username
sudo docker version
rm /etc/containerd/config.toml
systemctl restart containerd

```
