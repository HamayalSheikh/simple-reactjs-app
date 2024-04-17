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
                sh 'npm install' 
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t scdlab10 .'
            }
        }

        stage('Run Docker Image') {
            steps {
                sh 'docker run -d -p 8080:8080 scdlab10'
            }
        }

        stage('Push Docker Image') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'k12u', passwordVariable: 'DOCKER_PASSWORD', usernameVariable: 'DOCKER_USERNAME')]) {
                    sh '''
                        docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD
                        docker push your-image-name
                    '''
                }
            }
        }
    }
}
