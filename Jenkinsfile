//@Library('jenkins-shared-libraries@main') _
pipeline {
    agent any

   // environment {
     //   DOCKER_IMAGE_NAME = 'shaheen8954/nginx-project'
  //  }

    stages {
           stage('Cleanup Workspace') {
            steps {
                script {
                    cleanupWorkspace()
                }
            }
        }
        stage('welcome') {
            steps {
                echo "hello everyone"
            }
        }
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
              sh "docker run -d -p 80:80 nginx-project"
            }
        }
    }
}
