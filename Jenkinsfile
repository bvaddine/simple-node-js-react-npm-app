pipeline {
    agent any

    environment {
        NODE_VERSION = '8.16.1'
    }
    tools {nodejs "nodejs"}

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Install Dependencies') {
            steps {
                sh '''
                    curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.38.0/install.sh | bash
                    export NVM_DIR="$HOME/.nvm"
                    [ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"
                    nvm install 20.5.1
                    nvm use 20.5.1
                    npm install
                '''
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
