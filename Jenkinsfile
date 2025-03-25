pipeline {
    agent any
        stages {
            stage('Build') {
                steps {
                    echo 'Building...'
                    sh 'node -v'
                    sh 'npm -v'
                    sh 'npm run build'
                    sh 'ls'
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
