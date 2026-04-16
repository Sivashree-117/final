pipeline {
    agent any

    stages {

        stage('Clone Code') {
            steps {
                git 'https://github.com/Sivashree-117/final.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t sivashree117/royaltable:latest .'
            }
        }

        stage('Docker Login') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'docker',
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
                bat 'docker push sivashree117/royaltable:latest'
            }
        }

        stage('Run Container') {
            steps {
                bat 'docker run -d -p 8080:80 sivashree117/royaltable:latest'
            }
        }
    }
}
