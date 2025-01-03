pipeline {
    agent any

    environment {
        // Define environment variables for the project
        APP_NAME = "search-engine"
        MAVEN_HOME = tool name: 'Maven 3.9.9', type: 'ToolLocation'
        JAVA_HOME = tool name: 'JDK17', type: 'ToolLocation'
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from Git repository (ensure the branch is correct)
                git branch: 'main', url: 'https://github.com/farafatima44/jenkins.git'
            }
        }

        stage('Build') {
            steps {
                // Use Maven to build the application
                script {
                    bat '"${MAVEN_HOME}\\bin\\mvn" clean install'
                }
            }
        }

        stage('Unit Tests') {
            steps {
                // Run unit tests using Maven
                script {
                    bat '"${MAVEN_HOME}\\bin\\mvn" test'
                }
            }
        }

        stage('Package') {
            steps {
                // Package the application into a JAR file
                script {
                    bat '"${MAVEN_HOME}\\bin\\mvn" package'
                }
            }
        }

        stage('Deploy') {
            steps {
                // Deploy the application to your server or environment
                script {
                    def jarFile = "target\\${APP_NAME}-0.0.1-SNAPSHOT.jar"
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
                // Clean up workspace (optional)
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
