pipeline {
    agent any

    tools {
        nodejs 'NodeJS'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }

        stage('Build') {
            steps {
                bat 'echo Building project...'
                bat 'mkdir dist'
                bat 'echo Version 1.0.9 > dist/version.txt'
            }
        }

        stage('Test') {
            steps {
                bat 'npm test'
            }
        }

        stage('Package') {
            steps {
                bat 'powershell Compress-Archive -Path src -DestinationPath dist\\build.zip -Force'
            }
        }

        stage('Deploy (Simulation)') {
            steps {
                echo 'Deploying to simulated environment...'
            }
        }
    }

    post {
        always {
            echo 'Cleaning workspace...'
            cleanWs()
        }
        success {
            echo 'Pipeline succeeded! Version 1.0.9 built and tested.'
            echo '--- Submitted by: Muhammad Ahmad ---'
        }
        failure {
            echo 'Pipeline failed. Please check the logs.'
        }
    }
}
