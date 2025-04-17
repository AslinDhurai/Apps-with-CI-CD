pipeline {
    agent any
    tools {nodejs "NodeJS"}
    environment {
        GITHUB_CREDENTIALS = credentials('github-id') // GitHub credentials stored in Jenkins
        NODE_OPTIONS = "--openssl-legacy-provider"    // Fix OpenSSL issues in some Node.js versions
    }

    stages {
        stage('Build React App') {
            steps {
                script {
                    echo "Installing dependencies and building React app..."
                    sh '''
                        npm install
                        rm -rf build/
                        npm run build
                        ls -la build/
                    '''
                }
            }
        }

        stage('Deploy to Shared Directory') {
            steps {
                script {
                    echo "Copying React build files to /mnt/c/jenkins-share/react-build..."
                    sh '''
                        TARGET_DIR=/mnt/c/jenkins-share/react-build

                        mkdir -p $TARGET_DIR
                        rm -rf $TARGET_DIR/*
                        cp -r build/* $TARGET_DIR/
                        ls -la $TARGET_DIR
                    '''
                }
            }
        }
    }

    post {
        success {
            echo "✅ React app built and deployed to /mnt/c/jenkins-share/react-build!"
        }
        failure {
            echo "❌ Pipeline failed. Check logs for details."
        }
    }
}
