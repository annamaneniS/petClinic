pipeline {
  agent any
    environment {
      registry = "https://annamaneni.jfrog.io/"
      registryCredential = 'annamaneni_jfrog'
      dockerImage = ''
      //docker tag <IMAGE_ID> annamaneni.jfrog.io/petclinic-docker/<DOCKER_IMAGE>:<DOCKER_TAG>
      //docker push annamaneni.jfrog.io/petclinic-docker/<DOCKER_IMAGE>:<DOCKER_TAG>
      //docker pull annamaneni.jfrog.io/petclinic-docker/<DOCKER_IMAGE>:<DOCKER_TAG>
    }
  environment {
     imagename = " annamanenis/petclinic"
     registryCredential = 'dockerhub_annamaneni'
     dockerImage = ''
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
// Docker hub build and deploy
/* stage('Building image') {
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
    } */

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
