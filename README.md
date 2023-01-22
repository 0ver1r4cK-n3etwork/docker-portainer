<h1>docker and portainer installation w/ Debian 11 in english</h1>

### setup repository

1. remove docker on ur machine

  `
  sudo apt-get remove docker docker-engine docker.io containerd runc
  `

2. update and install packages

  `
  sudo apt-get update
  `
  
  ```
  sudo apt-get install \
  ca-certificates \
  curl \
  gnupg \
  lsb-release
  ```
  
3. create a keyrigs file and add docker's GPG key

  `sudo mkdir -p /etc/apt/keyrings`
  
  `curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg`
  
4. setup the repository

  ```
  echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
  ```
  
### install docker

1. update packages 
  
  `
  sudo apt-get update
  `
  
  /!\ IF U ARE A ERROR 
  
  /!\ `
  sudo chmod a+r /etc/apt/keyrings/docker.gpg
  `
  <br>
  /!\ `
  sudo apt-get update
  `
  
2. install docker

  `
  sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin
  `
  
3. run hello-world w/ docker for verify if docker his well installed

  `
  sudo docker run hello-world
  `
  
### install portainer

1. create volume for portainer

  `
  docker volume create portainer_data
  `
  
2. install portainer

> Community Edition

  `
  docker run -d -p 8000:8000 -p 9443:9443 --name portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:latest
  `
  
> Business Edition

  `
  docker run -d -p 8000:8000 -p 9443:9443 --name portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ee:latest
  `
  
 3. login to portainer
 
 `
 ip a
 `
 
 copy ur ipv4 address and paste to ur browser w/ port (9443)<br>
 <i>exemple: 192.168.1.55:9443</i>
