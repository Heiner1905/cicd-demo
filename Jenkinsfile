pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/Heiner1905/cicd-demo.git'
            }
        }
        stage('Build & Test') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Static Analysis (SonarQube)') {
            steps {
                sh '''
                    mvn sonar:sonar \
                      -Dsonar.projectKey=my-app \
                      -Dsonar.host.url=http://sonarqube:9000 \
                      -Dsonar.login=sqa_cc43b4599fc40bb9025a0a41aeed45b734f3aeaf
                '''
            }
        }
        stage('Docker Build') {
            steps {
                sh 'docker build -t mi-app:latest .'
            }
        }
        stage('Container Security Scan (Trivy)') {
            steps {
                sh 'trivy image --exit-code 1 --severity CRITICAL mi-app:latest'
            }
        }
        stage('Deploy') {
            when { branch 'main' }
            steps {
                sh 'docker run -d -p 80:8080 mi-app:latest'
            }
        }
    }
    post {
        failure {
            echo 'Pipeline falló — revisar logs'
        }
        always {
            echo 'Limpiando entorno...'
            cleanWs()
        }
    }
}