// Mock CI/CD pipeline for SIT753 Part 1 Task 2

pipeline {
    agent any

    environment {
        PATH = "/opt/homebrew/bin:${env.PATH}"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/ferdinand7103/8.2CDevSecOp.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'npm test || true'
            }
            post {
                always {
                    emailext(
                        to: 'your-email@gmail.com',
                        subject: "Jenkins - Run Tests Stage: ${currentBuild.currentResult} - Build #${env.BUILD_NUMBER}",
                        body: """
                            <p>Stage: <b>Run Tests</b></p>
                            <p>Status: <b>${currentBuild.currentResult}</b></p>
                            <p>Job: ${env.JOB_NAME} | Build: #${env.BUILD_NUMBER}</p>
                            <p>See attached log for details.</p>
                        """,
                        mimeType: 'text/html',
                        attachLog: true
                    )
                }
            }
        }

        stage('Generate Coverage Report') {
            steps {
                sh 'npm run coverage || true'
            }
        }

        stage('NPM Audit (Security Scan)') {
            steps {
                sh 'npm audit || true'
            }
            post {
                always {
                    emailext(
                        to: 'your-email@gmail.com',
                        subject: "Jenkins - NPM Audit Stage: ${currentBuild.currentResult} - Build #${env.BUILD_NUMBER}",
                        body: """
                            <p>Stage: <b>NPM Audit (Security Scan)</b></p>
                            <p>Status: <b>${currentBuild.currentResult}</b></p>
                            <p>Job: ${env.JOB_NAME} | Build: #${env.BUILD_NUMBER}</p>
                            <p>See attached log for details.</p>
                        """,
                        mimeType: 'text/html',
                        attachLog: true
                    )
                }
            }
        }
    }
}