pipeline {

  agent none

  stages{
    stage('SCM Checkout'){
      steps{
        git 'https://github.com/selipe16474/simple-java-maven-app.git'
        }
    }

    stage('Build and Compilation'){
      steps{
        sh "mvn clean package"
        }
    }

    stage('SonarQube Analysis'){
      steps{
        withSonarQubeEnv('sonar-7.1') {
        sh 'mvn sonar:sonar'
          }
        }
    }


     stage("Quality Gate") {
            steps {
                timeout(time: 1, unit: 'HOURS') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }


     stage('Test'){
      steps{
        archiveArtifacts artifacts: 'target/arctifacts/*.jar', fingerprint: true
        junit 'targets/junit-reports/*.xml'
          }
    }

     stage('Email Notification'){
      steps{
        mail bcc: '', body: 'Hi from Satya Elipe', cc: '', from: '', replyTo: '', subject: 'Hello from Jenkins...!!!', to: 'mrinn777@gmail.com'
          }
     }

  }

}
