pipeline {
    agent any

    environment {
        GITHUB_CREDENTIALS = credentials('github-id') // GitHub credentials stored in Jenkins
    }

    stages {
        stage('Build Application') {
            steps {
                script {
                    echo "Building the Spring Boot application..."
                    sh '''
                        mvn clean package
                        ls -la target/
                    '''
                }
            }
        }

        stage('Move JAR to Shared Directory') {
            steps {
                script {
                    echo "Moving the JAR file to shared directory for Windows access..."
                    sh '''
                        mkdir -p /mnt/c/jenkins-share/data
                        cp target/*.jar /mnt/c/jenkins-share/data/
                        ls -la /mnt/c/jenkins-share/data/
                    '''
                }
            }
        }

        stage('Restart Windows Service') {
            steps {
                script {
                    echo "Restarting Windows service hosting Spring Boot app..."
                    sh '''
                    cd /mnt/c/jenkins-share/data/
                    java -jar /mnt/c/jenkins-share/data/spring-boot-hello-world-example-0.0.1-SNAPSHOT.jar --server.port=9090 > app.log 2>&1 &
                    '''

                }
            }
        }
    }

    post {
        success {
            echo "Deployment complete. Application is running and reverse proxied by IIS."
        }
        failure {
            echo "Pipeline failed. Please check logs."
        }
    }
}
