@Librery ('jenkins-shared-libraries@main) _
pipeline {
    agent any

    stages {
        stage('Clone repo') {
            steps {
                git url: "https://github.com/Shaheen8954/nginx-project-1.git", branch: "main"
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
