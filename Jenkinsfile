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
 /* stage('Building image') {
        steps{
            script {
                dockerImage = docker.build imagename
            }
        }
    } */
    stage('Deploy Image') {
        steps{
            script {
              /*  docker.withRegistry( '', registryCredential ) {
                    dockerImage.push("$BUILD_NUMBER")
                    dockerImage.push('latest')
                }*/
                docker.withRegistry('https://annamaneni.jfrog.io', registryCredential) {
                  def dockerImage = docker.build("docker-local/spring-petclinic:${BUILD_NUMBER}", './')
                  dockerImage.push()
                  dockerImage.push('latest')
                }
            }
        }
    }
    stage('Jfrog Push') {
        steps{
            sh "docker rmi $imagename:$BUILD_NUMBER"
            sh "docker rmi $imagename:latest"
            /* sh "docker login -umythoughtsntalks@gmail.com annamaneni.jfrog.io"
            sh "docker tag spring-petclinic:2.7.0-SNAPSHOT  annamaneni.jfrog.io/petclinic-docker/spring-petclinic:2.7.0-SNAPSHOT"
            sh "docker push annamaneni.jfrog.io/petclinic-docker/spring-petclinic:2.7.0-SNAPSHOT" */
        }
    }
  }
}

