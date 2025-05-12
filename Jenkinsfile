//@Library('jenkins-shared-libraries@main') _
pipeline {
    agent any
    environment {
        DOCKER_IMAGE_NAME = 'shaheen8954/nginx-project'
        DOCKER_HUB_CREDS = "${env.DOCKER_HUB_USR}"
        DOCKER_PASSWORD = "${env.DOCKER_HUB_CREDS_PSW}"
    }

    stages {
        stage('Cleanup Workspace') {
            steps {
                cleanWs()
            }
        }

        stage('welcome') {
            steps {
                echo 'hello everyone'
            }
        }
        stage('Clone repo') {
            steps {
                checkout scm
            }
        }
        stage('Build image') {
            steps {
                sh 'docker build -t nginx-project .'
            }
        }
        stage('push image') {
            steps {
                sh 'docker tag nginx-project shaheen8954/nginx-project'
                // sh 'echo ${dockerpassword} | docker login -u ${dockerUser} --password-stdin'
                sh 'docker push shaheen8954/nginx-project'
            }
        }
        stage('Run container') {
            steps {
                sh 'docker stop $(docker ps -aq); docker rm $(docker ps -aq)'
                sh 'docker run -d -p 80:80 nginx-project'
            }
        }
    }
    post {
        success {
            mail to: 'nshaheen488@gmail.com',
                 subject: 'Testing done',
                 body: 'Hello, its done',
                 replyTo: 'nshaheen488@gmail.com'
        }
    }
}
