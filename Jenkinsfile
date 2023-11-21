pipeline {
    agent any
    tools {
        // Correct tool installation syntax
        maven 'maven_3_9_5'
    }
    stages {
        stage('Build Maven') {
            steps {
                // Correct syntax for the script block
                script {
                    // Checkout the source code
                    checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Arvind191/devops-automation']])

                    // Build the Maven project
                    sh 'mvn clean install'
                }
            }
        }
        stage('Build Docker image') {
            steps {
                // Correct syntax for the script block
                script {
                   sh 'docker build -t arvindkube/devops-integration .'
                }
            }
        }
        stage('Push image to Hub'){
            steps{
                script{
                    withCredentials([string(credentialsId: 'dockerhub-pwd', variable: 'dockerhubpwd')]) {
                    sh 'docker login -u arvindkube -p ${dockerhubpwd}'
}
                    sh 'docker push arvindkube/devops-integration'
                }
            }
        }
        // Add more stages as needed
    }
}