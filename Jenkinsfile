pipeline {
    agent any

    environment {
        GIT_CREDENTIALS = 'github-token' // Replace with your GitHub credentials ID if needed
    }

    stages {
        stage('Clone Repository') {
            steps {
                script {
                    git url: 'https://github.com/venkatsatish07/Bangalore_North0786.git', branch: 'main'
                }
            }
        }

        stage('Build') {
            steps {
                dir('complete') { // Navigate to 'complete' directory
                    echo 'Building the application...'
                    sh 'mvn clean package'
                }
            }
        }

        stage('Test') {
            steps {
                dir('complete') { // Navigate to 'complete' directory
                    echo 'Running tests...'
                    sh 'mvn test'
                }
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying the application...'
                // Assuming you have Kubernetes configuration files in the repo
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
