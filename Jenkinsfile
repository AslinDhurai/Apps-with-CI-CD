pipeline {
    agent any
    environment {
        GITHUB_CREDENTIALS = credentials('github-id')  // Use Jenkins credentials
    }
    stages {
        // stage('Clone Repository') {
        //     steps {
        //         script {
        //             checkout([$class: 'GitSCM',
        //                 branches: [[name: '*/spring']],
        //                 userRemoteConfigs: [[
        //                     url: "https://github.com/aslindhurai-cs/mine.git",
        //                     credentialsId: "github-id"
        //                 ]]
        //             ])
        //             sh 'pwd'  // Print current directory
        //             sh 'ls -la'  // List files to confirm repo is cloned
        //         }
        //     }
        // }
        stage('Build Application') {
            steps {
                script {
                    echo "Building the Spring Boot application..."
                    sh '''
                        pwd  # Print current directory
                        ls -la  # List files before build
                        # cd "4. spring-boot-hello-world-example"
                        mvn clean package
                        pwd  # Print directory after build
                        ls -la target/  # List files in target folder
                    '''
                }
            }
        }
        stage('Move JAR to Data Directory') {
            steps {
                script {
                    echo "Moving the generated JAR file to 'data' directory..."
                    sh '''
                        # cd "4. spring-boot-hello-world-example"
                        mkdir -p data  # Create data folder if it doesn't exist
                        mv target/spring-boot-hello-world-example-0.0.1-SNAPSHOT.jar data/
                        ls -la data/  # Verify JAR file is moved
                    '''
                }
            }
        }
        stage('Run Application') {
            steps {
                script {
                    echo "Running the Spring Boot application..."
                    sh '''
                        # cd "4. spring-boot-hello-world-example/data"
                        cd "data"
                        pwd  # Confirm correct directory
                        ls -la  # List files before running the JAR
                        nohup java -jar spring-boot-hello-world-example-0.0.1-SNAPSHOT.jar > app.log 2>&1 &
                        echo $! > app.pid  # Store process ID
                        ls -la  # Verify log and PID file are created
                        java -jar spring-boot-hello-world-example-0.0.1-SNAPSHOT.jar --server.port=9090
                    '''
                }
            }
        }
    }
    post {
        success {
            echo "Application started successfully!"
        }
        failure {
            echo "Build or execution failed!"
        }
    }
}
