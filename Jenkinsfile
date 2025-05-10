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
               sh "docker build -t nginx-project ."
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
