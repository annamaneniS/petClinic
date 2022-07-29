pipeline {
    agent any
    stages {
        stage ('Clone') {
            steps {
                git branch: 'dockerize_jfrog', url: "https://github.com/annamaneniS/petClinic.git"
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
         bat 'mvn clean install'
         echo "Junit test execution done"
      }
    }
        stage ('Artifactory configuration') {
            steps {
                rtServer (
                    id: "annamaneni",
                    url: "https://annamaneni.jfrog.io",
                    credentialsId: 'dockerhub_annamaneni'
                )
            }
        }

        stage ('Build docker image') {
            steps {
                script {
                    docker.build("spring-petclinic:latest")
                }
            }
        }

        stage ('Push image to Artifactory') {
            steps {
                rtDockerPush(
                    serverId: "annamaneni",
                    image: "spring-petclinic:latest",
                    host: "tcp://localhost:2375",
                    targetRepo: "petclinic-docker",
                    properties: "project-name=petclinic;status=stable"
                )
            }
        }

        stage ('Publish build info') {
            steps {
                rtPublishBuildInfo (
                    serverId: "annamaneni"
                )
            }
        }
    }
}
