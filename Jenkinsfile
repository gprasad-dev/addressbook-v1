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
                s3Upload(
                    file: 'target/addressbook.war', 
                    bucket: 'declarative-s3-bucket-jenkins',
                    acl: 'Private'
                )
            }
        }        
    }
}
