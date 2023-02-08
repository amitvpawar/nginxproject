pipeline {
    agent any

    stages {
        stage('SCM') {
            agent { label 'ansible' }
            steps {
                git 'https://github.com/amitvpawar/nginxproject.git'
                sh 'ansible-playbook copy.yml'
            }
        }
        stage('image-build') {
            steps {
                sh '''cd /home/amit/All/Jenkins/
                ls
                sudo docker build -t nginxtest .'''
            }
        }
        stage('running-container') {
            steps {
                sh '''sudo docker run -d --name nginxcont -p 8989:80 nginxtest
'''
            }
        }
        stage('testing') {
            steps {
                sh 'curl localhost:8989'
            }
        }
    }
}
