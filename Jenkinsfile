pipeline {
    environment {
        registry = "gm367/comp367lab3q1"
        registryCredential = 'dockerhub_id'
        dockerImage = ''
        }
    agent any
    
    tools {
        // Install the Maven version configured as "Maven-3" and add it to the path.
        maven "Maven-3"
    }

    stages {
        stage('Build') {
            steps {
                git 'https://github.com/YourGithubAccount/YourGithubRepository.git'
                }
        }
        
        stage('Build Docker Image') {
            steps{
                script {
                    dockerImage = docker.build registry + ":$BUILD_NUMBER"
                }
            }
        }
        stage('Push Image to Docker Hub') {
            steps{
                script {
                    docker.withRegistry( '', registryCredential ) {
                        dockerImage.push()
                    }
                }
            }
        }
        stage('Cleaning up') {
            steps{
                sh "docker rmi $registry:$BUILD_NUMBER"
            }
        }
    }
}
