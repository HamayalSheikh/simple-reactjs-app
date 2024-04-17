pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Dependency Installation') {
            steps {
                bat 'npm install' 
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t scdlab10'
            }
        }

        stage('Run Docker Image') {
            steps {
                bat 'docker run -d -p 8080:8080 scdlab10'
            }
        }

        stage('Push Docker Image') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'k12u', passwordVariable: 'DOCKER_PASSWORD', usernameVariable: 'DOCKER_USERNAME')]) {
                    bat '''
                        docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD
                        docker push your-image-name
                    '''
                }
            }
        }
    }
}


