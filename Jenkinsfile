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
                sh 'sudo python3 -m venv venv'
                sh 'sudo . venv/bin/activate'
                sh 'sudo make install'
                sh 'sudo wget -O /bin/hadolint https://github.com/hadolint/hadolint/releases/download/v1.16.3/hadolint-Linux-x86_64'
                sh 'sudo chmod +x /bin/hadolint'
            }
        }
        stage('Test') {
            steps {
                sh 'sudo . venv/bin/activate'
                sh 'make lint'
            }
        }
    }
}