pipeline {
    agent any
    stages {
        stage('Demo') {
            steps {
                echo 'Testing Extended Email Plugin…'
            }
            post {
                always {
                    emailext(
                        to: 'ahnafshahriardip@gmail.com',
                        subject: "Email-ext Test – ${currentBuild.fullDisplayName}",
                        body: """<p>Hello Ahnaf,</p>
                                 <p>This is a test email sent from the
                                 <b>Extended Email plugin</b>.</p>
                                 <p>Build result: ${currentBuild.currentResult}</p>""",
                        attachLog: true
                    )
                }
            }
        }
    }
}
