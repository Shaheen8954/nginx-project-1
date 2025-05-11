//@Library('jenkins-shared-libraries@main') _
pipeline {
    agent any

   // environment {
     //   DOCKER_IMAGE_NAME = 'shaheen8954/nginx-project'
  //  }

    stages {
           stage('Cleanup Workspace') {
               steps {
                   cleanWs()
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
              sh 'docker stop $(docker ps -aq); docker rm $(docker ps -aq)'
              sh "docker run -d -p 80:80 nginx-project"
            }
        }
    }
}
