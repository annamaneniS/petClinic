pipeline {
  agent any
   tools {
          maven 'Maven 3.3.9'
          jdk 'jdk8'
      }
  stages {
    stage ('Initialize') {
      steps {
         sh '''
          echo "PATH = ${PATH}"
          echo "M2_HOME = ${M2_HOME}"
           '''
         }
      }
    stage('Build') {
       steps {
         echo "Build started"
         sh 'mvn clean compile'
       }
    }
    stage('Test') {
      steps {
         echo "Test started"
      }
    }
    stage('Deploy') {
        steps {
            echo "Deployment started"
        }
    }

    post{
        always{
            mail to : mythoughtsntalks@gmail.com
        }

    }
  }
}
