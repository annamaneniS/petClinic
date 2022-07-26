pipeline {
  environment {
    registry = ""
    registryCredential = 'docker-hub'
    dockerImage = ''
  }
  agent any
  tools {
    maven 'Maven 3.3.9'
    jdk 'jdk8'
  }
  stages {
    stage('Cloning Git') {
      steps {
        git 'https://github.com/annamaneniS/petClinic.git'
      }
    }
    stage('Compile') {
       steps {
         sh 'mvn compile' //only compilation of the code
       }
    }
    stage('Test') {
      steps {
        sh '''
        mvn clean install
        ls
        pwd
        '''
      }
    }
    stage('Building Image') {
      steps{
        script {
          dockerImage = docker.build registry + ":latest"
        }
      }
    }
    stage('Deploy Image') {
      steps{
         script {
            docker.withRegistry( '', registryCredential ) {
            dockerImage.push()
          }
        }
      }
    }
    stage('Remove Unused docker image') {
      steps{
        sh "docker rmi $registry:latest"
      }
    }
  }
}
