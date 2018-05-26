pipeline {

  node any

  stages{
    stage('SCM Checkout'){
      git https://github.com/selipe16474/simple-java-maven-app.git
    }

    stage('Build'){
    def mvnHome = tool name: 'maven-3.5.3', type: 'maven'
    sh ${mvnHome/bin/mvn} clean package

    }

  }



}
