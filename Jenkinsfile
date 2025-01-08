pipeline {
    agent any
    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'master', url: 'https://github.com/gjain24/flask-hello-world.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t flask-docker-app .'
                }
            }
        }
        stage('Run Docker Container') {
            steps {
                script {
                    // Stop existing container (if any)
                    sh 'docker ps -q --filter name=flask-app | xargs --no-run-if-empty docker stop'
                    sh 'docker ps -aq --filter name=flask-app | xargs --no-run-if-empty docker rm'
                    // Run new container
                    sh 'docker run -d -p 80:80 --name flask-app flask-docker-app'
                }
            }
        }
    }
}
