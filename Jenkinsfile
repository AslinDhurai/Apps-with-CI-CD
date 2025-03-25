pipeline {
    agent any  // This runs the pipeline on any available agent

    stages {
        stage('Check Directory') {
            steps {
                script {
                    // Run 'ls' command to list files in the current directory
                    sh 'ls -l'
                }
            }
        }
    }
}
