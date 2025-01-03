pipeline {
    agent any

    environment {
        APP_NAME = "search-engine"
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from Git repository
                git 'https://github.com/farafatima44/jenkins.git'
            }
        }

        stage('Build & Test') {
            steps {
                // Run Maven build and tests in one step
                script {
                    bat 'mvn clean install' // For Unix/Linux-based systems
                    // bat '"C:/Program Files/apache-maven-3.9.9/bin/mvn" clean install' // For Windows-based systems
                }
            }
        }

        stage('Package') {
            steps {
                // Package the application
                script {
                    bat 'mvn package' // For Unix/Linux-based systems
                    // bat '"C:/Program Files/apache-maven-3.9.9/bin/mvn" package' // For Windows-based systems
                }
            }
        }

        stage('Deploy') {
            steps {
                // Deploy the application by running the JAR file
                script {
                    def jarFile = "target/${APP_NAME}-0.0.1-SNAPSHOT.jar"
                    if (fileExists(jarFile)) {
                        bat "java -jar ${jarFile}" // For Unix/Linux-based systems
                        // bat "java -jar target\\${APP_NAME}-0.0.1-SNAPSHOT.jar" // For Windows-based systems
                    } else {
                        error "JAR file not found. Deployment failed."
                    }
                }
            }
        }
    }

    post {
        success {
            echo "Build and deployment successful!"
        }
        failure {
            echo "Build or deployment failed!"
        }
    }
}
