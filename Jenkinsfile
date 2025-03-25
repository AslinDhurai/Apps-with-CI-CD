pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', credentialsId: 'github-id', url: 'https://github.com/aslindhurai-cs/mine.git'
            }
            steps{
                sh 'ls'
        }
    }
}
