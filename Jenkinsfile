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
                 wget -O /bin/hadolint https://github.com/hadolint/hadolint/releases/download/v1.16.3/hadolint-Linux-x86_64
                 chmod +x /bin/hadolint
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