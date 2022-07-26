pipeline {
  agent any

  stages {
     stage ('Initialize') {
            steps {
                bat '''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
                '''
            }
        }
    stage('Build') {
       steps {
         echo "Build started"
         bat 'mvn clean compile'
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
  }
}
