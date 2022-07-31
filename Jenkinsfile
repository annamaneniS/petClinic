pipeline {
  agent any
  environment {
     registryCredential = 'annamaneni_jfrog'
     dockerImage =  'petclinic-docker-local/petclinic'
     artifactoryURL ='https://annamaneni.jfrog.io'
     //docker tag spring-petclinic:latest  annamaneni.jfrog.io/petclinic-docker/spring-petclinic:latest
     //docker push annamaneni.jfrog.io/petclinic-docker/spring-petclinic:latest
  }
  stages {
    stage('Build binaries') {
       steps {
         echo "Build started"
         bat 'mvn clean compile'
       }
    }
    stage('Test binaries') {
      steps {
         echo "Test started"
         bat 'mvn clean install'
         echo "Junit test execution done"
      }
    }

    stage('Build and Deploy Image') {
        steps{
         echo "Build and Deploy Image to jfrog artifactory"
            script {
                docker.withRegistry(artifactoryURL, registryCredential) {
                  def dockerImage = docker.build(dockerImage:$BUILD_NUMBER, './')
                  dockerImage.push()
                  dockerImage.push('latest')
                }
            }
        }
    }
   /*  stage('Remove Unused docker image') {
         steps{
             sh "docker rmi $artifactoryURL/petclinic-docker/petclinic:latest"
         }
    } */
  }
}

