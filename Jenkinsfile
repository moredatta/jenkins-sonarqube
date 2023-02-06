pipeline{
    agent any
    tools {
    maven 'M3'
  }
    stages{
       stage('build && SonarQube analysis') {
            steps {
                withSonarQubeEnv('sonarqube-8.9.10') {
                    // Optionally use a Maven environment you've configured already
                   
                        sh 'mvn clean package sonar:sonar'
                   
                }
            }
       }
       
    }
}
