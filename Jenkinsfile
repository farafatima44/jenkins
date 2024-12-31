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
                // Checkout the code from Git repository
                git 'https://github.com/farafatima44/jenkins.git'
            }
        }

        stage('Build') {
            steps {
                // Use Maven to build the application
                script {
                    bat "'$C:/Program Files/apache-maven-3.9.9/bin/mvn/bin/mvn' clean install"
                }
            }
        }

        stage('Unit Tests') {
            steps {
                // Run unit tests using Maven
                script {
                    bat "'$C:/Program Files/apache-maven-3.9.9/bin/mvn/bin/mvn' test"
                }
            }
        }

        stage('Package') {
            steps {
                // Package the application into a JAR file
                script {
                    bat "'$C:/Program Files/apache-maven-3.9.9/bin/mvn' package"
                }
            }
        }

        stage('Deploy') {
            steps {
                // Deploy the application to your server or environment
                // Here we assume deploying to a local server as an example
                script {
                    bat "java -jar target\\${APP_NAME}-0.0.1-SNAPSHOT.jar"

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
