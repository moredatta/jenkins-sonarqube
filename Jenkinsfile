pipeline{
    agent any
    tools {
    maven 'M3'
  }
    stages{
       stage('build && SonarQube analysis') {
            steps {
                withSonarQubeEnv('sonarqube-10.1') {
                    // Optionally use a Maven environment you've configured already
                   
                        sh 'mvn clean package sonar:sonar'
                   
                }
            }
       }
     //   stage("Quality gate") {
      //      steps {
     //           waitForQualityGate abortPipeline: true
     //       }
    //    }
       
    }
}
