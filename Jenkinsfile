pipeline {

  agent any

  stages{
    stage('Checkout SCM'){
      steps{
        git 'https://github.com/selipe16474/simple-java-maven-app.git'
        }
    }

    stage('Build and Compilation'){
      steps{
        sh "mvn clean package"
        }
    }

    stage('Test'){
     steps{
       sh 'mvn test'
         }
      post{
        always{
          junit 'target/surefire-reports/*.xml'
          archiveArtifacts artifacts: 'target/arctifacts/*.jar', fingerprint: true
        }
      }

    }

    stage('SonarQube Analysis'){
      steps{
        withSonarQubeEnv('sonar-7.1') {
        sh 'mvn sonar:sonar'
          }
        }
    }

    stage("Sonar Quality Gate Check") {
            steps {
                timeout(time: 2, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
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
