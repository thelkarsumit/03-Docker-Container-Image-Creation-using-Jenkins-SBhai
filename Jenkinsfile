pipeline {
    agent any
    tools {
        maven 'Maven'
    }
     environment {
      SCANNER_HOME=tool 'SonarQube-Scanner'
      }
 stages {
       stage('sonarqube-analysis') {
           steps {
               withSonarQubeEnv('sonar-server') {
                   sh 'mvn clean verify sonar:sonar \
                       -Dsonar.projectKey=03-Docker-Container \
                       -Dsonar.host.url=http://35.228.202.17:9000 \
                       -Dsonar.login=sqp_e99f09f4ef01a6da391d903b0a9dd127ffa058aa'
             }
             }
        }
 }    
