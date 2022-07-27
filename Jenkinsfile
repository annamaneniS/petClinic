pipeline {
  agent any
   environment {
      registry = "https://annamaneni.jfrog.io/"
      registryCredential = 'AKCp8mZn5aEtjS2wMUGFzLY5FZKHcQoGo7eRLWeyCM3uMee16w67TNQJAqECE2jaQn3m9nWX4'
      dockerImage = 'petclinic'
    }
  stages {
    stage('Build') {
       steps {
         echo "Build started"
         bat 'mvn clean compile'
       }
    }
    stage('Test') {
      steps {
         echo "Test started"
         bat 'mvn clean install'
         echo "Junit test execution done"
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
