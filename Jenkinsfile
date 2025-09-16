pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                // Clones the new email demo repo
                git branch: 'main', url: 'https://github.com/Ahnaf-Shahriar-Dip/jenkins-email-demo.git'
            }
        }

        stage('Build & Test') {
            steps {
                echo 'Simulating a build process...'
                bat 'dir' // Lists files to simulate work
            }
        }

        stage('Random Outcome Stage') {
            steps {
                script {
                    // This stage will randomly pass or fail to demonstrate both email types
                    def random = new Random()
                    if (random.nextBoolean()) {
                        echo "This stage passed!"
                    } else {
                        error("This stage failed randomly for demonstration!")
                    }
                }
            }
            // POST-STAGE ACTION: Send an email after this specific stage
            post {
                always {
                    echo 'Random Stage completed. Sending stage-specific notification.'
                    emailext (
                        subject: "STAGE ALERT: ${currentBuild.fullDisplayName} - ${currentBuild.currentResult}",
                        to: "ahnafshahriar534@gmail.com", // REPLACE WITH YOUR EMAIL
                        body: """
                        The 'Random Outcome Stage' has finished.

                        Job: ${env.JOB_NAME}
                        Build Number: ${env.BUILD_NUMBER}
                        Stage Status: ${currentBuild.currentResult}
                        Build URL: ${env.BUILD_URL}

                        See attached log for details.
                        """,
                        attachLog: true,
                        compressLog: true
                    )
                }
            }
        }
    }

    // This POST section runs after ALL stages are completed
    post {
        always {
            echo 'Pipeline completed. Sending final summary email.'
            archiveArtifacts artifacts: '**/*.log', allowEmptyArchive: true
        }
        success {
            emailext (
                subject: "SUCCESS: ${env.JOB_NAME} - Build #${env.BUILD_NUMBER}",
                to: "ahnafshahriar534@gmail.com", // REPLACE WITH YOUR EMAIL
                body: """
                Congratulations! The pipeline was successful.

                Job: ${env.JOB_NAME}
                Build Number: ${env.BUILD_NUMBER}
                Build URL: ${env.BUILD_URL}

                All stages passed successfully.
                """,
                attachLog: true,
                compressLog: true
            )
        }
        failure {
            emailext (
                subject: "FAILED: ${env.JOB_NAME} - Build #${env.BUILD_NUMBER}",
                to: "ahnafshahriar534@gmail.com", // REPLACE WITH YOUR EMAIL
                body: """
                The pipeline has failed!

                Job: ${env.JOB_NAME}
                Build Number: ${env.BUILD_NUMBER}
                Build URL: ${env.BUILD_URL}

                Please check the attached log for error details and investigate.
                """,
                attachLog: true,
                compressLog: true
            )
        }
    }
}
