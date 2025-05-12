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

        stage('push to dockerhub') {
            steps {
                withCredentials([usernamePassword(
                credentiaksId: "dockerHubCreds",
                usernameVeriable: "dockerHubUser",
                passwordVeriable: "dockerHubPass")]){
                sh 'echo $dockerHubPass | docker login -u $dockerHubUser --password-stdin'
                sh "docker tag nginx-project ${env.dockerHubUser}/nginx-project"
                sh "docker push ${dockerHubUser}/nginx-project"
            }
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

        failure {
            mail to: 'nshaheen488@gmail.com',
                 subject: 'Testing done',
                 body: 'Hello, its fail',
                 replyTo: 'nshaheen488@gmail.com'
        }
    }
}
