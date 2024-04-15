pipeline {
    agent any

    stages {
        // stage('Checkout') {
        //     steps {
        //         // Checkout code from GitHub
        //         git 'https://github.com/Durrami/Jenkins.git/'
        //     }
        // }
        stage('Dependency Installation') {
            steps {
                // Install frontend dependencies (assuming npm)
                sh 'npm install'
            }
        }
        stage('Build Docker Image') {
            steps {
                // Build Docker image
                script {
                    docker.build("your-image-name:latest", "-f Dockerfile .")
                }
            }
        }
        stage('Push Docker Image to Docker Hub') {
            steps {
                // Push Docker image to Docker Hub
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'docker-hub-credentials') {
                        docker.image("your-image-name:latest").push("latest")
                    }
                }
            }
        }
        stage('Run Docker Image') {
            steps {
                // Run Docker image (assuming Docker Compose)
                sh 'docker-compose up -d'
            }
        }
    }

    post {
        always {
            // Cleanup
            script {
                // Stop and remove containers after use
                sh 'docker-compose down'
            }
        }
    }
}
