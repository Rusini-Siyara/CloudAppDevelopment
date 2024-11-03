pipeline {
    agent any

    stages {
        // Stage 1: Checkout the code from GitHub repository
        stage('Checkout') {
            steps {
                // Pulls code from the specified GitHub repository
                git url: 'https://github.com/Rusini-Siyara/CloudAppDevelopment.git', branch: 'main'
            }
        }

        // Stage 2: Build Docker Image
        stage('Build') {
            steps {
                script {
                    // Connects to the Docker daemon and builds an image named 'cloudapp-image'
                    docker.withServer('unix:///var/run/docker.sock') {
                        docker.build('cloudapp-image')
                    }
                }
            }
        }

        // Stage 3: Test the Docker Image
        stage('Test') {
            steps {
                script {
                    // Runs the 'cloudapp-image' in a container for testing purposes
                    docker.withServer('unix:///var/run/docker.sock') {
                        docker.image('cloudapp-image').inside {
                            // Replace with actual test commands if needed
                            sh 'echo "Running tests..."'
                        }
                    }
                }
            }
        }

        // Stage 4: Deploy the Docker Image
        stage('Deploy') {
            steps {
                script {
                    // Runs the 'cloudapp-image' as a background container on port 80
                    docker.withServer('unix:///var/run/docker.sock') {
                        docker.image('cloudapp-image').run('-d -p 80:80')
                    }
                }
            }
        }
    }
}

