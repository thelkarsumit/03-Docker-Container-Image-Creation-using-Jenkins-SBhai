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
                withSonarQubeEnv('SonarQube-server') {
                 sh 'mvn clean verify sonar:sonar \
                     -Dsonar.projectKey=03-Docker-Container-Shrameshwar-code \
                     -Dsonar.host.url=http://35.228.202.17:9000 \
                     -Dsonar.login=sqp_db2b1db52107b66b7f02e602eb3b94fd5f7e51af'
                }
            }
        }
        stage('Build') {
            steps {
                // Define steps for the Build stage
                echo 'Building the project...'
                sh 'mvn clean package'
            }
        }
        stage('Test') {
            steps {
                // Define steps for the Test stage
                echo 'Running tests...'
                sh 'mvn test'
            }
        }
    }
    post {
        success {
            // Actions to take if the pipeline succeeds
            echo 'Pipeline succeeded!'
            // You can also send an email notification on success
            mail to: 'thelkarsc@gmail.com',
                 subject: "Pipeline Succeeded: ${currentBuild.fullDisplayName}",
                 body: "The pipeline ${env.BUILD_URL} has successfully completed."
        }
        failure {
            // Actions to take if the pipeline fails
            echo 'Pipeline failed!'
            // You can also send an email notification on failure
            mail to: 'thelkarsc@gmail.com',
                 subject: "Pipeline Failed: ${currentBuild.fullDisplayName}",
                 body: "The pipeline ${env.BUILD_URL} has failed. Check the logs for details."
        }
    }
}
