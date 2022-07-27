pipeline {
  agent any
  environment {
     imagename = "annamanenis/petclinic"
     registryCredential = 'dockerhub_annamaneni'
     dockerImage = ''
      //docker tag annamaneni/petclinic  annamaneni.jfrog.io/petclinic-docker/annamaneni/petclinic:latest
      //docker push annamaneni.jfrog.io/petclinic-docker/annamanenis/petclinic:latest
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

  }
}
