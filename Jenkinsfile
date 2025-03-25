pipeline {
    agent any
    
    tools {nodejs "NodeJS"}
    
    environment {
        NODE_OPTIONS = "--openssl-legacy-provider"  // Fix potential build issues
        REACT_APP_PORT = "3000"  // Port for React app
    }

    stages {
        // stage('Clone Repository') {
        //     steps {
        //         git branch: 'main', credentialsId: 'github-id', url: 'https://github.com/yourusername/your-repo.git'
        //     }
        // }

        stage('Check Node.js and npm Versions') {
            steps {
                sh 'node -v'
                sh 'npm -v'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Build React App') {
            steps {
                sh 'npm run build'
            }
        }

        stage('Run React App') {
            steps {
                script {
                    // Start React app in the background and ensure it binds to 0.0.0.0
                    sh 'npm start &'
                    
                    // Wait for the app to start (adjust sleep time if necessary)
                    sleep(time: 30, unit: 'SECONDS')
                    
                    // Check if the React app is up (optional)
                    sh 'curl http://localhost:$REACT_APP_PORT'  // This checks if the app is running
                }
            }
        }
    }

    post {
        success {
            echo 'React app successfully deployed!'
        }
        failure {
            echo 'Build failed. Please check logs!'
        }
    }
}
