@Library('jenkins-shared-libraries@main') _
pipeline {
    agent any

    environment {
        DOCKER_IMAGE_NAME = 'shaheen8954/nginx-project'
    }

    stages {
           stage('Cleanup Workspace') {
            steps {
                script {
                    cleanupWorkspace()
                }
            }
        }
        stage('Clone repo') {
            steps {
                checkout scm
            }
        }
        stage('Build image') {
            steps {
                docker-build()
            }
        }
        stage('Run container') {
            steps {
              runDockerImage()
            }
        }
    }
}
