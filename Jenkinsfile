pipeline {
    agent any
    
    environment{
        dockerImage=''
        registry="pavankalyan18/dockerimage"
        registryCredential="dockerhub_id"
    }

    stages {
        stage('checkout'){
            steps{
                checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Pavan1831/DockerProject']])
            }
        }
        
        stage('Build Docker Image'){
            steps{
                script{
                    dockerImage=docker.build registry
                }
            }
        }
        
        stage('Push Docker Image'){
            steps{
                script{
                    docker.withRegistry('',registryCredential){
                        dockerImage.push()
                    }
                }
            }
        }
        
        stage('Run DockerImage'){
            steps{
                script{
                    bat "docker run %registry%"
                }
            }
        }
        
    }
}