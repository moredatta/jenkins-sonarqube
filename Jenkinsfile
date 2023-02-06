pipeline{
    agent any
    tools {
    maven 'M3'
  }
    stages{
       stage('Build'){
            steps{
                sh 'mvn clean package'
            }
         }
        stage('SonarQube analysis') {
//    def scannerHome = tool 'SonarScanner 4.0';
        steps{
        withSonarQubeEnv('sonarqube-8.9.10') { 
        // If you have configured more than one global server connection, you can specify its name
//    sh"${scannerHome}/bin/sonar-scanner"
      sh "mvn sonar:sonar"
    }
        }
        }
       
    }
}
