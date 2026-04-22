pipeline {
    agent any

    tools {
        maven 'Maven'
    }

    environment {
        IMAGE_NAME = "pranvdhumal909/emp1"
        TAG = "v1"
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Pranavdhumal100/Employee1.git'
            }
        }

        stage('Build') {
            steps {
                bat 'mvn clean package'
            }
        }

        stage('Test') {
            steps {
                bat 'mvn test'
            }
        }

        stage('Docker Build') {
            steps {
                bat 'docker build -t %IMAGE_NAME%:%TAG% .'
            }
        }

        stage('Docker Push') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-creds',
                    usernameVariable: 'pranvdhumal909',
                    passwordVariable: 'dckr_pat_fnNYk2vQrH2EWqAD78yg4nk726U
'
                )]) {
                    bat '''
                        echo %PASS% | docker login -u %USER% --password-stdin
                        docker push %IMAGE_NAME%:%TAG%
                    '''
                }
            }
        }
    }
}