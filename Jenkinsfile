pipeline {
  agent any
  environment {
     imagename = "spring-petclinic"
     registryCredential = 'annamaneni_jfrog'
     dockerImage = ''
     //docker tag spring-petclinic:2.7.0-SNAPSHOT  annamaneni.jfrog.io/petclinic-docker/spring-petclinic:2.7.0-SNAPSHOT
     //docker push annamaneni.jfrog.io/petclinic-docker/spring-petclinic:2.7.0-SNAPSHOT
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
   stage('Build image') { // build and tag docker image
         steps {
             echo 'Starting to build docker image'

             script {
                 def dockerfile = 'Dockerfile'
                 def customImage = docker.build('annamaneni.jfrog.io/petclinic-docker/annamaneni/petclinic:latest ', "-f ${dockerfile} .")

             }
         }
     }

     stage ('Push image to Artifactory') { // take that image and push to artifactory
         steps {
             rtDockerPush(
                 serverId: "jFrog-ar1",
                 image: "annamaneni.jfrog.io/petclinic-docker/annamaneni/petclinic:latest",
                 host: 'tcp://localhost:2375',
                 targetRepo: 'petclinic-docker-remote', // where to copy to (from docker-virtual)
                 properties: 'project-name=docker1;status=stable'
             )
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
