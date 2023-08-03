pipeline {
    agent any
    
    tools {
        maven 'M3'
    }
  
    environment {
        EMAIL_TO = 'dattatray@bioenabletech.com'
        REPORT_FILE = 'failure_report.txt' // File to store the failure report
    }
    
    stages {
        stage('Scan with Probely') {
            steps {
                // Replace 'probelyScan' with the correct Probely code scanning step
                // For example: probelyScan(targetId: 'YOUR_TARGET_ID', credentialsId: 'probly-test')
                // Replace 'YOUR_TARGET_ID' with your actual Probely target ID
                probelyScan targetId: '9nl6yy0TWWKv', credentialsId: 'probly-test'	
            }
        }
    }
    
    post {
        always {
            sh 'echo "this is testing"'
        }
        failure {
            // Generate a failure report
            script {
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
