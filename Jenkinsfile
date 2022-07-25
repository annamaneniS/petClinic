pipeline {
    agent any
    tools {
        maven 'Maven 3.8.6'
        jdk 'jdk8'
    }
    stages {
        stage('Build') {
            steps {
                echo 'Build PetClinic'
                sh 'mvn clean install'
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
