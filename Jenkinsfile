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
                echo 'Running Tests…'
            }
            post {
                always {
                    emailext(
                        to: 'ahnafshahriardip@gmail.com',
                        subject: "Jenkins: Test Stage ${currentBuild.currentResult}",
                        body: """<p>The Test stage finished with status: <b>${currentBuild.currentResult}</b>.</p>
                                 <p>Full console log attached.</p>""",
                        attachLog: true
                    )
                }
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Running Security Scan…'
            }
            post {
                always {
                    emailext(
                        to: 'ahnafshahriardip@gmail.com',
                        subject: "Jenkins: Security Scan ${currentBuild.currentResult}",
                        body: """<p>Security scan finished with status: <b>${currentBuild.currentResult}</b>.</p>
                                 <p>Full console log attached.</p>""",
                        attachLog: true
                    )
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
