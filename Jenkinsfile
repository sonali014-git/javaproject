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
                export KUBECONFIG=/var/lib/jenkins/.kube/config

                echo "Checking Kubernetes connection..."
                kubectl get nodes

                echo "Deploying application..."
                kubectl apply -f deployment.yaml --validate=false
                kubectl apply -f service.yaml --validate=false

                echo "Checking pods and services..."
                kubectl get pods
                kubectl get svc
                '''
            }
        }
    }
}
