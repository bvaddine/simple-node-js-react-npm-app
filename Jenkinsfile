pipeline {
    agent any

    environment {
        NODE_VERSION = '14'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Install Dependencies') {
            steps {
                sh "nvm install ${NODE_VERSION}"
                sh "nvm use ${NODE_VERSION}"
                sh 'npm install'
            }
        }

        stage('Unit Test') {
            steps {
                sh 'npm test'
            }
        }

        stage('Build') {
            steps {
                sh 'npm run build'
            }
        }

        stage('Deploy') {
            steps {
                sh 'npm run deploy:staging'
            }
        }
    }
    
    post {
        success {
            echo 'Web application deployed to staging successfully!'
        }
        
        failure {
            echo 'Web application deployment to staging failed!'
        }
    }
}
