pipeline {
    agent any

    environment {
        NODE_OPTIONS = "--openssl-legacy-provider"
    }

    stages {
        stage('Checkout Code') {
            steps {
                script {
                    try {
                        git branch: 'master', 
                            credentialsId: 'github-id', 
                            url: 'https://github.com/aslindhurai-cs/mine.git'
                    } catch (Exception e) {
                        error "❌ Git Checkout Failed: ${e.message}"
                    }
                }
            }
        }

        stage('Check Node & npm Version') {
            steps {
                script {
                    try {
                        sh 'node -v'
                        sh 'npm -v'
                    } catch (Exception e) {
                        error "❌ Node.js or npm Not Found: ${e.message}"
                    }
                }
            }
        }

        stage('Check React & Dependencies') {
            steps {
                script {
                    try {
                        sh 'npx react-scripts --version || echo "React-scripts not found!"'
                        sh 'npm list react || echo "React not installed!"'
                    } catch (Exception e) {
                        error "❌ React Check Failed: ${e.message}"
                    }
                }
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
                sh 'nohup npm start &'
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
