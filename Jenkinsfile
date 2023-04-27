pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                // Checkout source code from version control
                checkout scm

                // Build with Maven
                sh 'mvn clean install'
            }
        }

        stage('SonarQube') {
            steps {
                // Run SonarQube analysis
                withSonarQubeEnv('SonarQubeServer') {
                    sh 'mvn sonar:sonar'
                }
            }
        }

        stage('Docker Build') {
            steps {
                // Build Docker image
                sh 'docker build -t your-image-name .'
            }
        }

        stage('Docker Push') {
            steps {
                // Push Docker image to Docker registry
                sh 'docker push your-image-name'
            }
        }

        stage('Docker Deploy') {
            steps {
                // Deploy Docker container to Docker host or Kubernetes
                sh 'docker run -d -p 8080:8080 your-image-name'
            }
        }
    }
}
