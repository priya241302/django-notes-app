pipeline {
    agent any

    stages {
        stage('Clone') {
            steps {
                echo 'Clone the code from Github'
                git url: 'https://github.com/priya241302/django-notes-app.git',branch:'main'
            }
        }
        
         stage('Build') {
            steps {
                echo 'Build code'
                sh 'docker build -t my-note-app .'
            }
        }
         stage('Push') {
            steps {
                echo 'Push the code to dockerhub'
                withCredentials([usernamePassword(credentialsId:'dockerHub',passwordVariable:'PASS',usernameVariable:'USER')]){
                sh '''docker tag my-note-app ${USER}/my-note-app:latest '''
                sh '''docker login -u ${USER} -p ${PASS}'''
                sh '''docker push ${USER}/my-note-app:latest'''
                
                }
            }
        }
         stage('Deploy') {
            steps {
                echo 'deploy the code'
                sh 'docker-compose down && docker-compose up -d'
            }
        }
    }
}
