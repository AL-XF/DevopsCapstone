pipeline {
    environment {
        registry = "liiwza/capstone"
        registryCredential = 'dockerhub'
        dockerImage = ''
    }
    agent any

    stages {
        stage('Build') {
            agent {
                    docker { image 'python:3.7.3-stretch'}
                }
            steps {
                sh 'python3 -m venv venv'
                sh """
                . venv/bin/activate
                 make install
                 """
            }
        }
        stage('Test') {
            steps {
                sh 'python3 -m venv venv'
                sh """
                . venv/bin/activate
                make install
                make lint
                """
            }
        }
        stage('Build Image') {
            steps{
                script {
                dockerImage = docker.build registry + ":$BUILD_NUMBER"
                }
            }
        }
        stage('Deploy to Docker Hub') {
            steps{
                script {
                    docker.withRegistry( '', registryCredential ) {
                        dockerImage.push()
                    }
                }
            }
        }
        stage('Remove Unused docker image') {
            steps{
                sh "docker rmi $registry:$BUILD_NUMBER"
            }
        }
    }
}