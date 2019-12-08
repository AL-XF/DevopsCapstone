pipeline {
    environment {
        registry = "liiwza/capstone"
        registryCredential = 'dockerhub'
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
                sh """
                . venv/bin/activate
                make lint
                """
            }
        }
    }
}