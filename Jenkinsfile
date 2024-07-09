pipeline {
    agent any

    environment {
        GIT_CREDENTIALS = credentials('github-token') // Replace 'github-token' with your Jenkins credentials ID
    }

    stages {
        stage('Clone Repository') {
            steps {
                script {
                    git credentialsId: GIT_CREDENTIALS, url: 'https://github.com/venkatsatish07/gs-spring-boot.git', branch: 'main'
                }
            }
        }

        stage('Build') {
            steps {
                dir('complete') {
                    echo 'Building the application...'
                    sh 'mvn clean package'
                }
            }
        }

        stage('Test') {
            steps {
                dir('complete') {
                    echo 'Running tests...'
                    sh 'mvn test'
                }
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying the application...'
                sh 'kubectl apply -f k8s/deployment.yaml'
                sh 'kubectl apply -f k8s/service.yaml'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
