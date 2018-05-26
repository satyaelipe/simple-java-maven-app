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
        //def mvnHome = tool name: 'maven-3.5.3', type: 'maven'
        sh "mvn clean package"
          }

    }

  }

}
