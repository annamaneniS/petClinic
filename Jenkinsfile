pipeline {
  agent any
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
      }
    }
    stage('Deploy') {
        steps {
            echo "Deployment started"
            bat './mvnw spring-boot:build-image'
        }
    }
  }
}
