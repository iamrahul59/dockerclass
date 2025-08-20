pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                // Checkout the source code from the GitHub repository
                checkout scm
            }
        }

        stage('Clean Up Docker') {
            steps {
                script {
                    // Stop and remove all Docker containers
                    sh '''
                    docker stop $(docker ps -q) || true
                    docker rm $(docker ps -a -q) || true
                    '''
                }
            }
        }

        stage('Deploy with Docker Compose') {
            steps {
                script {
                    // Deploy the application using docker-compose
                    sh 'docker compose up -d'
                }
            }
        }

        stage('Verify Deployment') {
            steps {
                script {
                    // Optionally verify the deployment
                    sh 'docker ps'
                }
            }
        }
    }

    post {
        success {
            // Actions to perform if the pipeline succeeds
            echo 'Deployment succeeded!'
        }
        failure {
            // Actions to perform if the pipeline fails
            echo 'Deployment failed!'
        }
        always {
            // Actions to always perform, regardless of success or failure
            echo 'Cleaning up Workspace'
            cleanWs()
        }
    }
}
