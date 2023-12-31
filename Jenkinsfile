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
 git branch: 'main', url: 'https://github.com/sharath005/Ekarttest.git'
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
Dsonar.login=squ_6449b6d4f427a75c224bfd63361e7cc8ffc73034 -
Dsonar.projectName=Ekartest \
 -Dsonar.java.binaries=. \
 -Dsonar.projectKey=Ekartest '''
 }
 }
