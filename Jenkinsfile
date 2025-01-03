pipeline {
    agent any

    environment {
        APP_NAME = 'search-engine'
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from the repository
                git 'https://github.com/farafatima44/jenkins.git'
            }
        }

        stage('Build and Test') {
            steps {
                // Use Maven to clean, build, and test all in one step
                bat 'mvn clean install'
            }
        }

        stage('Package') {
            steps {
                // Package the application into a JAR file
                bat 'mvn package'
            }
        }

        stage('Deploy') {
            steps {
                // Deploy the application by running the JAR file
                script {
                    def jarFile = "target/${APP_NAME}-0.0.1-SNAPSHOT.jar"
                    if (fileExists(jarFile)) {
                        bat "java -jar ${jarFile}"
                    } else {
                        error "JAR file not found. Deployment failed."
                    }
                }
            }
        }

        stage('Cleanup') {
            steps {
                // Clean up the workspace after deployment
                cleanWs()
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
