pipeline{
    agent any
    environment {
        PATH = "$PATH:C:/Program Files/Apache Software Foundation/Tomcat 10.0/bin"
    }
    stages{
       stage('Build'){
            steps{
                bat 'mvn clean package'
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