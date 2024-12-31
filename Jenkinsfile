pipeline {
    agent any

    environment {
        // Define environment variables for the project
        APP_NAME = "product-search-service"
        MAVEN_HOME = tool name: 'M3', type: 'ToolLocation'
        JAVA_HOME = tool name: 'JDK11', type: 'ToolLocation'
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from Git repository
                git 'https://github.com/your-username/your-repo.git'
            }
        }

        stage('Build') {
            steps {
                // Use Maven to build the application
                script {
                    sh "'${MAVEN_HOME}/bin/mvn' clean install"
                }
            }
        }

        stage('Unit Tests') {
            steps {
                // Run unit tests using Maven
                script {
                    sh "'${MAVEN_HOME}/bin/mvn' test"
                }
            }
        }

        stage('Package') {
            steps {
                // Package the application into a JAR file
                script {
                    sh "'${MAVEN_HOME}/bin/mvn' package"
                }
            }
        }

        stage('Deploy') {
            steps {
                // Deploy the application to your server or environment
                // Here we assume deploying to a local server as an example
                script {
                    sh "java -jar target/${APP_NAME}-0.0.1-SNAPSHOT.jar &"
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
