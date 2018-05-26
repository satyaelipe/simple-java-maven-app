pipeline {
  
  agent any
  
  stages{
    stage('SCM Checkout'){
      steps{
        git 'https://github.com/selipe16474/simple-java-maven-app.git'
        }
    }

    stage('Build and SonarQube Analysis'){
      steps{
        withMaven(maven:'Maven 3.5.3') {
        sh 'mvn clean package sonar:sonar'
        //sh "mvn clean package"
          }
        }
    }
      
     stage("Quality Gate") {
            steps {
                timeout(time: 1, unit: 'HOURS') {
                    // Parameter indicates whether to set pipeline to UNSTABLE if Quality Gate fails
                    // true = set pipeline to UNSTABLE, false = don't
                    // Requires SonarQube Scanner for Jenkins 2.7+
                    waitForQualityGate abortPipeline: true
                }
            }
        }
      
      
     stage('Test'){
      steps{
        archiveArtifacts artifacts: 'Users/selipe/.jenkins/workspace/**/*.jar', fingerprint: true
        junit 'Users/selipe/.jenkins/workspace/**/*.xml'
          }
    }
    
     stage('Email Notification'){
      steps{
        mail bcc: '', body: '', cc: '', from: '', replyTo: '', subject: 'Hello from Jenkins...!!!', to: 'mrinn777@gmail.com'
          }
     }

  }
  
}
