pipeline {
    agent any
    environment {
        JD_IMAGE = 'cloudapp-image' // Define the Docker image name here
    }
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
                    // Debugging step to confirm JD_IMAGE is set correctly
                    echo "Building Docker image with name: ${env.JD_IMAGE}"

                    // Connects to the Docker daemon and builds an image named 'cloudapp-image'
                    docker.withServer('unix:///var/run/docker.sock') {
                        docker.build(env.JD_IMAGE)
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
                        docker.image(env.JD_IMAGE).inside {
                            // Replace with actual test commands if needed
                            sh 'echo "Running tests..."'
                        }
                    }
                }
            }
        }
    }
}
