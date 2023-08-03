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
                probelyScan targetId: '9nl6yy0TWWKv', credentialsId: 'probly-test'	
            }
        }
    }
    
    post {
        always {
            sh 'echo "this is testing"'
        }
        success {
            // Send an email notification on pipeline success (if needed)
            emailext body: "Jenkins pipeline for code scanning with SonarQube was successful.",
                     subject: "Jenkins Pipeline - Code Scanning Success",
                     to: "${EMAIL_TO}" // Replace with the email address to receive success notifications
        }
        failure {
            // Generate a failure report
            script {
                sh 'echo "Failure Report:" > ${REPORT_FILE}'
                sh 'echo "Pipeline failed due to code quality issues." >> ${REPORT_FILE}'
                sh 'echo "Job URL: ${BUILD_URL}" >> ${REPORT_FILE}'
                // Add more relevant information to the report if needed
            }
            
            // Quality gate with waitForQualityGate step and a timeout of 1 minute
            timeout(time: 1, unit: 'MINUTES') {
                script {
                    def qg = waitForQualityGate abortPipeline: true
                    if (qg.status != 'OK') {
                        currentBuild.result = 'FAILURE'
                    }
                }
            }
            
            // Send an email notification on pipeline failure with the failure report attached
            emailext body: "Jenkins pipeline for code scanning with SonarQube has failed. Please review and fix the issues.\nJob URL: ${BUILD_URL}",
                     subject: "Jenkins Pipeline - Code Scanning Failure",
                     to: "${EMAIL_TO}", // Replace with the email address to receive failure notifications
                     attachmentsPattern: "${REPORT_FILE}" // Attach the generated report to the email
        }
    }
}
