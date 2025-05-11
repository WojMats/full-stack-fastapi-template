pipeline {
    agent any

    environment {
        COMPOSE_PROJECT_NAME = "ci_pipeline"
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Kod źródłowy pobrany automatycznie przez Jenkins.'
            }
        }

        stage('Build and Start Containers') {
            steps {
                sh 'docker compose -f docker-compose.yml up -d --build'
            }
        }

        stage('Run Backend Tests') {
            steps {
                dir('backend') {
                    sh 'docker run --rm --env-file ../.env backend-ci pytest'
                }
            }
        }

        stage('Stop Containers') {
            steps {
                sh 'docker compose -f docker-compose.yml down'
            }
        }

        stage('Success') {
            steps {
                echo 'Pipeline zakończony powodzeniem.'
            }
        }
    }

    post {
        failure {
            echo 'Pipeline nie powiódł się.'
        }
    }
}
