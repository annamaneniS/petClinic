pipeline {
    agent any
    stages {
        stage ('Clone') {
            steps {
                git branch: 'dockerize_jfrog', url: "https://github.com/annamaneniS/petClinic.git"
            }
        }

        stage ('Artifactory configuration') {
            steps {
                rtServer (
                    id: "annamaneni",
                    url: "https://annamaneni.jfrog.io/",
                    credentialsId: 'annamaneni_jfrog'
                )
            }
        }

        stage ('Build docker image') {
            steps {
                script {
                    docker.build("https://annamaneni.jfrog.io/petclinic-docker" + '/spring-petclinic:latest', '')
                }
            }
        }

        stage ('Push image to Artifactory') {
            steps {
                rtDockerPush(
                    serverId: "annamaneni",
                    image: "https://annamaneni.jfrog.io" + '/spring-petclinic:latest',
                    // Host:
                    // On OSX: "tcp://127.0.0.1:1234"
                    // On Linux can be omitted or null
                    host: HOST_NAME,
                    targetRepo: 'petclinic-docker',
                    // Attach custom properties to the published artifacts:
                    properties: 'project-name=petclinic;status=stable'
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
