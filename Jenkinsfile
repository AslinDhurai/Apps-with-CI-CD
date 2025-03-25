pipeline {
    agent any
    environment {
        NODE_OPTIONS = "--openssl-legacy-provider"
    }
        stages {
            stage('Build') {
                steps {
                    echo 'Building...'
                    sh 'node -v'
                    sh 'npm -v'
                    sh 'ls'
                    sh 'rm -rf node_modules package-lock.json'
                    sh 'ls'
                    // sh 'export NODE_OPTIONS=--openssl-legacy-provider'
                    sh 'echo $NODE_OPTIONS'
                    sh 'npm install'
                    sh 'npm start'
                    sh 'npm run build'

                }
            }
            stage('Test') {
                steps {
                    echo 'Testing...'
                    sh 'npm test'
                }
        }
    }
}
