pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "sivashree117/royaltable"
    }

    stages {

        stage('Clone Code') {
            steps {
                git branch: 'main', url: 'https://github.com/Sivashree-117/final.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t %DOCKER_IMAGE%:latest .'
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
                bat 'docker push %DOCKER_IMAGE%:latest'
            }
        }

        stage('Run Container') {
            steps {
                bat '''
                docker stop royaltable || true
                docker rm royaltable || true
                docker run -d -p 8081:80 --name royaltable %DOCKER_IMAGE%:latest
                '''
            }
        }
    }
}
