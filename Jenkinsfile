pipeline {
  agent any
  environment {
    // imagename = "spring-petclinic"
     registryCredential = 'annamaneni_jfrog'
    // dockerImage = ''
     //docker tag spring-petclinic:2.7.0-SNAPSHOT  annamaneni.jfrog.io/petclinic-docker/spring-petclinic:2.7.0-SNAPSHOT
     //docker push annamaneni.jfrog.io/petclinic-docker/spring-petclinic:2.7.0-SNAPSHOT
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
            script {
                docker.withRegistry('https://annamaneni.jfrog.io', registryCredential) {
                  def dockerImage = docker.build("petclinic-docker-local/spring-petclinic:${BUILD_NUMBER}", './')
                  dockerImage.push()
                  dockerImage.push('latest')
                }
            }
        }
    }
  }
}

