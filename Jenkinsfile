pipeline {
    agent any

    stages {
        stage('git checkout') {
            steps {
                git credentialsId: 'cred-git', url: 'https://github.com/gprasad-dev/addressbook-v1.git'
            }
        }
        stage('compilitation the code') {
            steps {
                sh 'mvn compile'
            }
        }
        stage('code review') {
            steps {
                sh 'pwd'
            }
        }
    }
}
