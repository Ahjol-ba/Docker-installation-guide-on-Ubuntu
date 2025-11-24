# DIGU
Docker installation guide on Ubuntu

## Before all, remove default docker component on system，
```
sudo apt-get remove docker docker-engine docker.io containerd runc
```

## Install necessary dependence
```
sudo apt install apt-transport-https ca-certificates curl software-properties-common gnupg lsb-release
```

## Config GPG key 
```
curl -fsSL https://mirrors.aliyun.com/docker-ce/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```

## Instead apt default source with aliyun 
```
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://mirrors.aliyun.com/docker-ce/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

## update
```
sudo apt update && sudo apt-get update
```

## Install Docker
```
sudo apt install docker-ce docker-ce-cli containerd.io
```

## Check out version
```
sudo docker version
```

## Check out running status
```
sudo systemctl status docker
```

## [option] Install Command Completion Tool
```
sudo apt-get install bash-completion && \
sudo curl -L https://raw.githubusercontent.com/docker/docker-ce/master/components/cli/contrib/completion/bash/docker -o /etc/bash_completion.d/docker.sh && \
source /etc/bash_completion.d/docker.sh
```

## Allow Non-root user excute docker command
```
sudo groupadd docker && \
sudo usermod -aG docker $USER && \
echo "newgrp docker &>/dev/null" >> ~/.bashrc && \
source ~/.bashrc && \
sudo systemctl restart docker
```

## Config daemon
1.Open file
```
sudo nano /etc/docker/daemon.json
```
2.Edit the file
```
"registry-mirrors": [
    "https://xxx" # Your source address. Could purchase from https://xuanyuan.cloud/
  ]
```
3.estart service
```
sudo systemctl deamon-reload && \
sudo systemctl restart docker
```
