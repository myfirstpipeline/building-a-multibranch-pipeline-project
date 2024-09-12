pipeline {
    agent {
        docker {
            image 'node:latest'  // Use the Node.js Docker image
            args '-u root:root'  // Optional: Run as root or specified user if needed
        }
    }
    environment {
        CI = 'true'  // Maintain the environment variable
    }
    stages {
        stage('Build') {
            steps {
                sh 'npm install'  // Command to install npm dependencies
            }
        }
        stage('Test') {
            steps {
                sh './jenkins/scripts/test.sh'  // Command to run the test script
            }
        }
        stage('Deliver for development') {
            when {
                branch 'development'
            }
            steps {
                sh './jenkins/scripts/deliver-for-development.sh'
                input message: 'Finished using the web site? (Click "Proceed" to continue)'
                sh './jenkins/scripts/kill.sh'
            }
        }
        stage('Deploy for production') {
            when {
                branch 'production'
            }
            steps {
                sh './jenkins/scripts/deploy-for-production.sh'
                input message: 'Finished using the web site? (Click "Proceed" to continue)'
                sh './jenkins/scripts/kill.sh'
            }
        }        
    }
}
