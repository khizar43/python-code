pipeline {

    agent any

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/khizar43/python-code.git'
            }
        }

        stage('Run Python') {
            steps {
                bat 'python python.py'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t python-app:v1 .'
            }
        }
    }
}
