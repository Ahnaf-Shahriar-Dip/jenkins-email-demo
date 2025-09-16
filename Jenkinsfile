pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building…'
            }
        }
        stage('Test') {
            steps {
                echo 'Running tests…'
            }
            post {
                always {
                    // Send email at end of Test stage
                    mail to: 'ahnafshahriardip@gmail.com',
                         subject: "Jenkins Test Stage: ${currentBuild.currentResult}",
                         body: """The Test stage finished with status: ${currentBuild.currentResult}.
Full console output: ${env.BUILD_URL}console"""
                }
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Running security scan…'
            }
            post {
                always {
                    // Send email at end of Security Scan stage
                    mail to: 'ahnafshahriardip@gmail.com',
                         subject: "Jenkins Security Scan: ${currentBuild.currentResult}",
                         body: """Security scan finished with status: ${currentBuild.currentResult}.
Full console output: ${env.BUILD_URL}console"""
                }
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying…'
            }
        }
    }
}
