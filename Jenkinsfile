pipeline {
    agent any

    tools {
        maven 'Maven'
    }

    stages {

        stage('Build') {
            steps {
                dir('demo') {
                    sh 'mvn clean package'
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

        stage('Docker Login') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockercreds', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                    sh 'docker login -u $USER -p $PASS'
                }
            }
        }

        stage('Docker Push') {
            steps {
                sh 'docker push sonalidocker/java-app'
            }
        }
    }
}
