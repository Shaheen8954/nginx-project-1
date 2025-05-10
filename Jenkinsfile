@Library ('jenkins-shared-libraries@main') _
pipeline {
    agent any

    environment {
        DOCKER_IMAGE_NAME = 'nginx-project'
        
    stages {
        stage('Clone repo') {
            steps {
                checkout scm
            }
        }
        stage('Build image') {
            steps {
               docker-build(nginx-project', 'latest')
            })   
            }
        }
        stage('Run container') {
            steps {
               runDockerImage(env.DOCKER_IMAGE_NAME)  
            }
        }
     }
  }
}
