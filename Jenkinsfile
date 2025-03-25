pipeline {
    agent any
        stages {
            stage('Build') {
                steps {
                    echo 'Building...'
                    sh 'node -v'
                    sh 'npm -v'
                    sh 'ls'
                    sh 'rm -rf node_modules'
                    sh 'ls'
                    sh 'export NODE_OPTIONS=--openssl-legacy-provider'
                    sh 'npm install'
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
