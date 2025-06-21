# wscicd
Workshop CiCd

Install docker

Java
sudo apt-get install openjdk-8-jre-headless


Jenkins
wget http://mirrors.jenkins.io/war-stable/latest/jenkins.war

Executar
java -jar Jenkins.war &

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
