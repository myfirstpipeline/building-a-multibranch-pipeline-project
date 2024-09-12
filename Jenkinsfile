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
    }
}
