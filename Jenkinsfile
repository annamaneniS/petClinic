pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Build PetClinic'
                sh "mvn clean install"
            }
        }

        stage('Test') {
            steps {
                echo 'Test PetClinic'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploy PetClinic'
            }
        }
    }
}
