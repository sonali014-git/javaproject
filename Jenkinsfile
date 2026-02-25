pipeline {
    agent any

    stages {

        stage('Clean') {
            steps {
                deleteDir()
            }
        }

        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/sonali014-git/javaproject.git'
            }
        }

        stage('Build') {
            steps {
                dir('demo') {
                    sh 'mvn clean package'
                }
            }
        }

        stage('Check Dockerfile') {
            steps {
                dir('demo') {
                    sh 'cat Dockerfile'
                }
            }
        }

        stage('Docker Build') {
            steps {
                dir('demo') {
                    sh 'docker build -t sonalidocker/java-app .'
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh '''
                kubectl apply -f deployment.yaml
                kubectl apply -f service.yaml
                '''
            }
        }
    }
}
