pipeline{
    agent any
    tools {
    maven 'M3'
  }
    stages{
       stage('build && SonarQube analysis') {
            steps {
                withSonarQubeEnv('sonarQube-8.9.20') {
                    // Optionally use a Maven environment you've configured already
                   
                        sh 'mvn clean package sonar:sonar'
                   
                }
            }
       }
        stage("Quality gate") {
            steps {
                waitForQualityGate abortPipeline: true
            }
        }
       
    }
}
