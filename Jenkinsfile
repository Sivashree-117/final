pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "sivashree117/royaltable"
        DOCKER_TAG = "latest"
    }

    stages {

        stage('Clone Code') {
            steps {
                git branch: 'main', url: 'https://github.com/Sivashree-117/final.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE:$DOCKER_TAG .'
            }
        }

        stage('Docker Login') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker', usernameVariable: 'sivashree117', passwordVariable: 'Sivashree@26')]) {
                    sh 'echo $PASS | docker login -u $USER --password-stdin'
                }
            }
        }

        stage('Push Image') {
            steps {
                sh 'docker push $DOCKER_IMAGE:$DOCKER_TAG'
            }
        }

        stage('Run Container') {
            steps {
                sh '''
                docker stop royaltable || true
                docker rm royaltable || true
                docker run -d -p 8080:80 --name royaltable $DOCKER_IMAGE:$DOCKER_TAG
                '''
            }
        }
    }
}
