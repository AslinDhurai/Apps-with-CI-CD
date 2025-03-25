pipeline {
    agent any

    environment {
        NODE_OPTIONS = "--openssl-legacy-provider"
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'master', 
                    credentialsId: 'github-id', // Use stored GitHub credentials
                    url: 'https://github.com/aslindhurai-cs/mine.git'
            }
        }

        stage('Check Node & npm Version') {
            steps {
                sh 'node -v'   // Check Node.js version
                sh 'npm -v'    // Check npm version
            }
        }

        stage('Check React & Dependencies') {
            steps {
                sh 'npx react-scripts --version || echo "React-scripts not found!"'  // Check React version
                sh 'npm list react || echo "React not installed!"'                   // Verify React is installed
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

        stage('Start React App') {
            steps {
                sh 'nohup npm start &' // Runs in the background
            }
        }
    }

    post {
        success {
            echo "✅ React app is running successfully!"
        }
        failure {
            echo "❌ Build failed. Check logs for errors!"
        }
    }
}
