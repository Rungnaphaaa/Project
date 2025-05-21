pipeline {
    agent any
    stages {
        // stage('Clone') {
        //     steps {
        //         git url: 'https://github.com/Rungnaphaaa/Project-Cloud.git', branch: 'main'
        //     }
        // }
        stage('Clean Containers') {
            steps {
                sh 'docker rm -f rabbitmq || true'
                sh 'docker rm -f user-db recipe-db favorite-db rating-db || true'
                sh 'docker compose --project-name project down frontend user-service recipe-service rating-service favorite-service api-gateway reverse-proxy'
            }
        }

        stage('Build Frontend and Services') {
            steps {
                sh 'docker compose --project-name project build frontend user-service recipe-service rating-service favorite-service api-gateway reverse-proxy'
            }
        }

        stage('Start Containers') {
            steps {
                sh 'docker compose --project-name project up -d frontend user-service recipe-service rating-service favorite-service api-gateway reverse-proxy'
            }
        }

        stage('Check Status') {
            steps {
                sh 'docker ps'
            }
        }
    }
}
