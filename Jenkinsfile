pipeline {
    agent any

    environment {
        IMAGE_NAME = "sivashree117/royaltable"
    }

    stages {

        stage('Clone Code') {
            steps {
                git branch: 'main', url: 'https://github.com/Sivashree-117/final.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat '''
                docker build -t %IMAGE_NAME%:latest .
                '''
            }
        }

        stage('Docker Login') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'docker-cred',
                    usernameVariable: 'sivashree117',
                    passwordVariable: 'Sivashree@26'
                )]) {
                    bat '''
                    echo %DOCKER_PASS% | docker login -u %DOCKER_USER% --password-stdin
                    '''
                }
            }
        }

        stage('Push Image') {
            steps {
                bat '''
                docker push %IMAGE_NAME%:latest
                '''
            }
        }

        stage('Run Container') {
            steps {
                bat '''
                docker stop royaltable-container || exit 0
                docker rm royaltable-container || exit 0
                docker run -d -p 8080:80 --name royaltable-container %IMAGE_NAME%:latest
                '''
            }
        }
    }
}
