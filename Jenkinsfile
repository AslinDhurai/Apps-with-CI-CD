pipeline {
    agent any
    tools {nodejs "NODEJS"}
        stages {
            stage('Build') {
                steps {
                    echo 'Building...'
                    sh 'npm install'
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
