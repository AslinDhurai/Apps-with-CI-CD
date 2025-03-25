pipeline {
    agent any
    
    tools {nodejs "NodeJS"}
    
    environment {
        NODE_OPTIONS = "--openssl-legacy-provider"  // Fix potential build issues
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
                sh 'npm start &'
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
