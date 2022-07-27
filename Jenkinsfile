pipeline {
  agent any
   /* environment {
      registry = "https://annamaneni.jfrog.io/"
      registryCredential = 'dockerhub_annamaneni'
      dockerImage = 'petclinic'
    } */
   environment {
     imagename = "annamanenis/petclinic"
     registryCredential = 'dockerhub_annamaneni'
     dockerImage = ''
    // registry = "https://annamaneni.jfrog.io/annamaneni/petclinic"
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
    stage('Building image') {
    steps{
    script {
    dockerImage = docker.build imagename
    }
    }
    }
    stage('Deploy Image') {
    steps{
    script {
    docker.withRegistry( '', registryCredential ) {
    dockerImage.push("$BUILD_NUMBER")
    dockerImage.push('latest')
    }
    }
    }
    }
    stage('Remove Unused docker image') {
    steps{
    sh "docker rmi $imagename:$BUILD_NUMBER"
    sh "docker rmi $imagename:latest"
    }
    }

    /*  stage('Building Image') {
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
        } */
  }
}
