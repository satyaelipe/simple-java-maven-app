pipeline {
  
  agent any
  
  stages{
    stage('SCM Checkout'){
      steps{
        git 'https://github.com/selipe16474/simple-java-maven-app.git'
        }
    }

    stage('Build'){
      steps{
        sh "mvn clean package"
          }
    }
      
     stage('Test'){
      steps{
        archiveArtifacts artifacts: '**/*.jar', fingerprint: true
        junit '**/*.xml'
          }
    }
    
     stage('Email Notification'){
      steps{
        mail bcc: '', body: '', cc: '', from: '', replyTo: '', subject: 'Hello from Jenkins...!!!', to: 'mrinn777@gmail.com'
          }
     }

  }
  
}
