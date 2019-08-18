pipeline {

  agent any

  stages{
    stage('Checkout SCM'){
      steps{
        git 'https://github.com/satyaelipe/simple-java-maven-app.git'
        }
    }

    stage('Build and Sonar Qube Analysis'){
      steps{
        withSonarQubeEnv('sonar-7.1'){
        sh "mvn clean package sonar:sonar"
        }
      }
    }

    stage("Sonar Quality Gate Check") {
       steps {
        timeout(time: 1, unit: 'HOURS') {
            waitForQualityGate abortPipeline: true
               }
           }
    }
      
    stage('Test'){
     steps{
       sh 'mvn test'
         }
      post{
        always{
          junit 'target/surefire-reports/*.xml'
          archiveArtifacts artifacts: 'target/**/*.jar', fingerprint: true
        }
      }
    }
      
    
    
    stage ('Deliver'){
      steps{
        sh './jenkins/scripts/deliver.sh'
      }
    }

    /* stage('Email Notification'){
      steps{
        mail bcc: '', body: 'Hi from Satya Elipe', cc: '', from: '', replyTo: '', subject: 'Hello from Jenkins...!!!', to: 'mrinn777@gmail.com'
          }
     } */

  }

}
