pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building…'
                // Example: tool: Maven or Gradle
            }
        }

        stage('Test') {
            steps {
                echo 'Running Tests…'
            }
            post {
                always {
                    emailext (
                        to: 'ahnafshahriar534@gmail.com',
                        subject: "Jenkins: Test Stage ${currentBuild.currentResult}",
                        body: "The Test stage finished with status: ${currentBuild.currentResult}",
                        attachmentsPattern: '**/test-output/*.log',
                        attachLog: true
                    )
                }
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Running Security Scan…'
                // e.g. tool: OWASP Dependency-Check
            }
            post {
                always {
                    emailext (
                        to: 'ahnafshahriar534@gmail.com',
                        subject: "Jenkins: Security Scan ${currentBuild.currentResult}",
                        body: "Security scan completed with status: ${currentBuild.currentResult}",
                        attachLog: true
                    )
                }
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying…'
                // e.g. tool: Ansible/Kubernetes
            }
        }
    }
}
