pipeline {
    agent any

    tools {
        gradle 'Gradle-test'
    }

    environment {
        EMAIL_TO = 'dattatray@bioenabletech.com'
        REPORT_FILE = 'failure_report.txt' // File to store the failure report
    }

    stages {
       // stage('Unit tests') {
      //      steps {
       //         sh './gradlew check'
       //     }
       // }
        stage('Scan with Probely') {
            steps {
                // Replace 'YOUR_TARGET_ID' with your actual Probely target ID
                probelyScan targetId: 'example1', credentialsId: 'probly-test', waitForScan: true, stopIfFailed: true, failThreshold: 'medium'
            }
        }
    }

    post {
        always {
            // Wrap the file operation in a node step
            node('') {
                sh 'echo "this is testing"'
            }
        }
        failure {
            // Wrap the file operations in a node step
            node('') {
                // Generate a failure report
                sh 'echo "Failure Report:" > ${REPORT_FILE}'
                sh 'echo "Pipeline failed due to code quality issues." >> ${REPORT_FILE}'
                sh 'echo "Job URL: ${BUILD_URL}" >> ${REPORT_FILE}'
                // Add more relevant information to the report if needed
            }

            // Send an email notification on pipeline failure with the failure report attached
            emailext body: "Jenkins pipeline for code scanning with Probely has failed. Please review and fix the issues.\nJob URL: ${BUILD_URL}",
                    subject: "Jenkins Pipeline - Code Scanning Failure",
                    to: "${EMAIL_TO}", // Replace with the email address to receive failure notifications
                    attachmentsPattern: "${REPORT_FILE}" // Attach the generated report to the email
        }
    }
}
pipeline {
    agent any

    environment {
        EMAIL_TO = 'dattatray@bioenabletech.com'
        REPORT_FILE = 'failure_report.txt' // File to store the failure report
    }

    stages {
        stage('Unit tests') {
            steps {
                sh './gradlew check'
            }
        }
        stage('Scan with Probely') {
            steps {
                // Replace 'YOUR_TARGET_ID' with your actual Probely target ID
                probelyScan targetId: '9nl6yy0TWWKv', credentialsId: 'probly-test', waitForScan: true, stopIfFailed: true, failThreshold: 'medium'
            }
        }
    }

    post {
        always {
            // Wrap the file operation in a node step
            node {
                sh 'echo "this is testing"'
            }
        }
        failure {
            // Wrap the file operations in a node step
            node {
                // Generate a failure report
                sh 'echo "Failure Report:" > ${REPORT_FILE}'
                sh 'echo "Pipeline failed due to code quality issues." >> ${REPORT_FILE}'
                sh 'echo "Job URL: ${BUILD_URL}" >> ${REPORT_FILE}'
                // Add more relevant information to the report if needed
            }

            // Send an email notification on pipeline failure with the failure report attached
            emailext body: "Jenkins pipeline for code scanning with Probely has failed. Please review and fix the issues.\nJob URL: ${BUILD_URL}",
                    subject: "Jenkins Pipeline - Code Scanning Failure",
                    to: "${EMAIL_TO}", // Replace with the email address to receive failure notifications
                    attachmentsPattern: "${REPORT_FILE}" // Attach the generated report to the email
        }
    }
}
