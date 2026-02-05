pipeline {
    agent any

    tools {
        nodejs 'nodejs'
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'master',
                    url: 'https://github.com/betawins/Trading-UI.git'
            }
        }

        stage('Verify Node & NPM') {
            steps {
                sh '''
                node -v
                npm -v
                '''
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Start Application with PM2') {
            steps {
                sh '''
                pm2 delete Trading-UI || true
                pm2 start npm --name Trading-UI -- start
                pm2 save
                '''
            }
        }
    }

    post {
        success {
            echo '✅ Trading-UI is running'
        }
        failure {
            echo '❌ Pipeline failed'
        }
    }
}

