@Library('jenkins-shared-libraries@main') _
pipeline {
    agent any
    environment {
        DOCKER_HUB_CREDS = credentials('dockerhub-cred')
        dockerUser = "${env.DOCKER_HUB_CREDS_USR}"
        dockerpassword = "${env.DOCKER_HUB_CREDS_PSW}"
    }

    stages {
        stage('Cleanup Workspace') {
            steps {
                cleanWs()
            }
        }

        stage('welcome') {
            steps {
                hello()
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
                sh "echo $dockerpassword | docker login -u $dockerUser --password-stdin"
                sh "docker tag nginx-project ${env.dockerUser}/nginx-project"
                sh "docker push ${env.dockerUser}/nginx-project"
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
                 body: 'Hello, the pipeline finished successfully!',
                 replyTo: 'nshaheen488@gmail.com'
        }

        failure {
            mail to: 'nshaheen488@gmail.com',
                 subject: 'Pipeline Failed',
                 body: 'Hello, the pipeline failed. Please check the Jenkins logs.',
                 replyTo: 'nshaheen488@gmail.com'
        }
    }
}
