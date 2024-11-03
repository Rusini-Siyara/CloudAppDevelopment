pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/Rusini-Siyara/CloudAppDevelopment.git', branch: 'main'
            }
        }
        stage('Build') {
            steps {
                script {
                    docker.withServer('unix:///var/run/docker.sock') {
                        docker.build('cloudapp-image')
                    }
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    docker.withServer('unix:///var/run/docker.sock') {
                        docker.image('cloudapp-image').inside {
                            sh 'echo "Running tests..."'
                            // Add your test commands here
                        }
                    }
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    docker.withServer('unix:///var/run/docker.sock') {
                        docker.image('cloudapp-image').run('-d -p 80:80')
                    }
                }
            }
        }
    }
}
