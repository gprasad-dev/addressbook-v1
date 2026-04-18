
pipeline {
    agent any

    stages {
        stage('git checkout') {
            steps {
                git 'https://github.com/gprasad-dev/addressbook-v1.git'
            }
        }
         stage('compilitation the code') {
            steps {
                sh 'mvn compile'
            }
        }
         stage('code review') {
            steps {
                sh 'mvn pmd:pmd'
            }
        }
        stage('Unit test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('package') {
            steps {
                sh 'mvn package'
            }
        }
        stage('Code coverage') {
            steps {
                sh 'mvn verify'
            }
        }
        stage('s3 bucket storing') {
            steps {
               s3Upload acl: 'Private', bucket: 'kubebytes-bucket-2006', file: '/var/lib/jenkins/workspace/abc/target/addressbook.war'
            }
        }
        
    }
}
