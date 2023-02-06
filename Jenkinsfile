pipeline{
    agent any
    stages{
       stage('Build'){
            steps{
                bat 'C:\Program Files\apache-maven-3.8.7\bin\mvn clean package'
            }
         }
        stage('SonarQube analysis') {
//    def scannerHome = tool 'SonarScanner 4.0';
        steps{
        withSonarQubeEnv('sonarqube-8.9.10') { 
        // If you have configured more than one global server connection, you can specify its name
//      bat "${scannerHome}/bin/sonar-scanner"
        bat "mvn sonar:sonar"
    }
        }
        }
       
    }
}
