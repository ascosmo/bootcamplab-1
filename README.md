# wscicd
Workshop CiCd

Install docker
- Criar container do Jenkins
docker run -it --name vm-java ubuntu:latest /bin/bash
apt update -y
apt install -y wget vim openjdk-17-jre-headless
wget http://mirrors.jenkins.io/war-stable/latest/jenkins.war
docker run -it -p 8080:8080 vm-java-jenkins /bin/bash
java -jar jenkins.war
Acessar no browser
localhost:8080


-------
- Criar container da aplicação.
docker build -t bootcamp .
docker run -it bootcamp -p 8080:80 /bin/bash
docker exec -it <container>

Java
sudo apt-get install openjdk-8-jre-headless


Jenkins
   wget http://mirrors.jenkins.io/war-stable/latest/jenkins.war

Executar
docker run -it -p 8080:80 df7e64353365 /bin/bash

Acessar <ip-da-vm:8080>

User do Jenkins = Andre - pass = 123

Criar job como pipeline

Pipeline

node {
   def mvnHome
   stage('Preparation') { // for display purposes
      // Get some code from a GitHub repository
      git 'https://github.com/ascosmo/bootcamplab.git'

   }
   stage('Docker Build') { // for display purposes
      // Get some code from a GitHub repository
      sh "sudo docker build -t myapp ."

   }
   stage('Parando a aplicação') { // for display purposes
      // Get some code from a GitHub repository
      sh label: '', script: 'sudo docker run hello-world;sudo docker stop $(sudo docker ps -a -q); sudo docker container prune -f'

   }
   stage('Realizando o Deploy'){
     sh "sudo docker run --name meusite -p 8082:80 -d myapp"
