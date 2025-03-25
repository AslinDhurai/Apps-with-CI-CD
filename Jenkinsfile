pipeline {
    agent any

    environment {
        NODE_VERSION = "16"  // Set the Node.js version
        NODE_OPTIONS = "--openssl-legacy-provider"  // Fix for OpenSSL issue
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'master', url: 'https://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@github.com/aslindhurai-cs/mine.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                script {
                    sh 'rm -rf node_modules package-lock.json'  // Remove old dependencies
                    sh 'npm cache clean --force'  // Clean npm cache
                    sh 'npm install --legacy-peer-deps'  // Install dependencies
                }
            }
        }

        stage('Build React App') {
            steps {
                script {
                    sh 'npm run build'  // Create optimized production build
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    sh 'npm test -- --watchAll=false'  // Run tests
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    sh 'cp -r build/* /var/www/html/'  // Copy build files to server directory
                }
            }
        }
    }

    post {
        success {
            echo '✅ Build and Deployment Successful!'
        }
        failure {
            echo '❌ Build Failed. Check logs for errors.'
        }
    }
}
