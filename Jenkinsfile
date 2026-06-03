pipeline {

    agent any

    environment {
         IMAGE_NAME = "khizaryounus/python-app"
        DOCKER_CREDS = credentials('dockerhub-creds')
    }


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
        stage('Install Dependencies') {
            steps {
                bat 'python -m pip install -r requirements.txt'
              }
          } 
        stage('test Python') {
            steps {
                bat 'pytest'
            }
        }

        stage("docker login"){
            steps {
                 bat '''
                docker login -u %DOCKER_CREDS_USR% -p %DOCKER_CREDS_PSW%
                '''
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t %IMAGE_NAME%:v1 .'
            }
        }
         stage('Push Image') {
            steps {
                bat 'docker push %IMAGE_NAME%:v1'
            }
        }
    } 
    
    post {
        success {
            echo 'Pipeline Successful'
        }

        failure {
            echo 'Pipeline Failed'
        }
    }
}
