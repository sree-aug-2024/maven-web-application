node{
  
def mavenHome = tool name: 'maven 3.9.8' 

stage('CheckoutCode'){
git branch: 'development', credentialsId: 'e0e5bd7d-6c7a-4b4e-939e-01cbb2226127', url: 'https://github.com/sree-aug-2024/maven-web-application.git'
}

stage('Build'){
sh "$mavenHome/bin/mvn clean package"
}

stage('ExecuteSonarQubeReport'){
sh "$mavenHome/bin/mvn clean sonar:sonar"
}

stage('UploadArtifactsIntoNexus'){
sh "$mavenHome/bin/mvn clean deploy"
}

stage('DeployAppIntoTomcat'){
sshagent(['8a41423e-f390-4be0-bada-2e42b8bcfa1d']) {
sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@172.31.5.228:/opt/apache-tomcat-9.0.95/webapps/"    
}
}


}


  
