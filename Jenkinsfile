pipeline {
    agent any

    stages {
        stage('Clone repo') {
            steps {
                echo 'Repo already cloned ręcznie'
            }
        }

        stage('Build backend Docker image') {
            steps {
                dir('backend') {
                    sh 'docker build -t backend-ci .'
                }
            }
        }

        stage('Run backend tests') {
            steps {
                dir('backend') {
                    sh 'docker run --rm backend-ci pytest'
                }
            }
        }

        stage('Success message') {
            steps {
                echo 'Pipeline zakończony sukcesem.'
            }
        }
    }
}
