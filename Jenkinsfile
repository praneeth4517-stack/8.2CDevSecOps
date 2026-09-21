pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/praneeth4517-stack/8.2CDevSecOps.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'npm install || exit /b 0'
            }
        }

        stage('Run Tests') {
            steps {
                bat 'npm test || exit /b 0'
                emailext (
                    subject: "Run Tests stage completed - Build #${env.BUILD_NUMBER}",
                    body: "The Run Tests stage has completed for build #${env.BUILD_NUMBER}. See attached log for details.",
                    to: 'praneeth4517@gmail.com',
                    attachLog: true
                )
            }
        }

        stage('Generate Coverage Report') {
            steps {
                bat 'npm run coverage || exit /b 0'
            }
        }

        stage('NPM Audit (Security Scan)') {
            steps {
                bat 'npm audit || exit /b 0'
                emailext (
                    subject: "Security Scan stage completed - Build #${env.BUILD_NUMBER}",
                    body: "The NPM Audit (Security Scan) stage has completed for build #${env.BUILD_NUMBER}. See attached log for details.",
                    to: 'praneeth4517@gmail.com',
                    attachLog: true
                )
            }
        }

    }
}
