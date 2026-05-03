pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/helderklemp/cicd-demo.git'
            }
        }
        stage('Build & Test') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Docker Build') {
            steps {
                sh 'docker build -t mi-app:latest .'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
    }
    post {
        always {
            echo 'Limpiando entorno...'
            cleanWs()
        }
    }
}