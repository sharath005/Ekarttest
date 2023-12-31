pipeline {
 agent any
tools {
 jdk 'jdk11'
 maven 'maven3'
 dockerTool 'docker'
}
environment{
 SCANNER_HOME= tool 'sonar-scanner'
}
 stages {
 stage('Git Checkout') {
 steps {
 git branch: 'main', url: 'https://github.com/Muruganv07/Ekart.git'
 }
 }
 stage('Complile'){
 steps{
 sh "mvn clean compile"
 }
 }
 stage('Sonarqube Analysis'){
 steps{
 sh ''' $SCANNER_HOME/bin/sonar-scanner -
Dsonar.url=http://13.201.80.6:9000/ -
Dsonar.login=squ_28fc0183e6afadc91e43e4673c3c7568699ddd19 -
Dsonar.projectName=Ekart \
 -Dsonar.java.binaries=. \
 -Dsonar.projectKey=Ekart '''
 }
 }
 stage('Build'){
 steps{
 sh "mvn clean install -DskipTests=true"
 }
 }
 stage('Docker Build & Push') {
 steps {
 script{
 withDockerRegistry(credentialsId: '11611aa2-590c-48a9-b4bf3d4437711e68', toolName: 'docker') {
 
 sh "docker build -t shopping-cart -f docker/Dockerfile ."
 sh "docker tag shopping-cart murugan1502/shopping-cart:latest"
 sh "docker push murugan1502/shopping-cart:latest"
 }
 }
 }
 }
 stage('Trigger'){
 steps{
 build job: "CD", wait: true
 }
 }
 
 }
}
