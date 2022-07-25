pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Build PetClinic'
                withMaven(maven : 'apache-maven-3.8.6') {
                      bat 'mvn clean install'
                }
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
