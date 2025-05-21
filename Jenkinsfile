pipeline {
    agent any
    stages {
        stage('Clone') {
            steps {
                git url: 'https://github.com/Rungnaphaaa/Project-Cloud.git', branch: 'main'
            }
        }
        stage('Clean Containers') {
            steps {
                sh 'docker compose --project-name cloud down frontend user-service recipe-service rating-service favorite-service api-gateway reverse-proxy'
            }
        }

        stage('Build Frontend and Services') {
            steps {
                sh 'docker compose --project-name cloud build frontend user-service recipe-service rating-service favorite-service api-gateway reverse-proxy'
            }
        }

        stage('Start Containers') {
            steps {
                sh 'docker compose --project-name cloud up -d frontend user-service recipe-service rating-service favorite-service api-gateway reverse-proxy'
            }
        }

        stage('Check Status') {
            steps {
                sh 'docker ps'
            }
        }
    }
}
