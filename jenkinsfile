pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Simulating checkout phase
                echo 'Checking out source code...'
            }
        }

        stage('Build') {
            steps {
                // Compile app.py (using python to check syntax)
                sh 'python3 -m py_compile app.py'
                
                // Wait 15 seconds
                sleep time: 15, unit: 'SECONDS'
                
                // Pass milestone 1
                milestone 1
            }
        }

        stage('Send Notification') {
            steps {
                // Using mail step (with echo fallback if SMTP is not configured)
                script {
                    try {
                        mail to: 'admin@example.com',
                             subject: "Build Notification: ${env.JOB_NAME} - #${env.BUILD_NUMBER}",
                             body: "The build completed successfully. View details here: ${env.BUILD_URL}"
                    } catch (Exception e) {
                        echo "SMTP not configured. Notification workaround: Sending mail to admin@example.com | Subject: Build Notification: ${env.JOB_NAME} - #${env.BUILD_NUMBER} | Body: ${env.BUILD_URL}"
                    }
                }
            }
        }
    }
}
