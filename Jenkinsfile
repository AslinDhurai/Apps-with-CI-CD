pipeline {
    agent any
        stages {
            stage('Build') {
                steps {
                    echo 'Building...'
                    sh 'node -v'
                    sh 'npm -v'
                    sh 'ls'
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
