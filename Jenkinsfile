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
                    bucket: 'declarative-pipeline-bucket-gyana',
                    file: 'target/addressbook.war',
                    acl: 'Private'
                )
            }
        }
        stage('Deploy the code to tomcat') {
            steps {
                sh 'cp /var/lib/jenkins/workspace/Declarative-pipeline-job/target/*.war /home/ubuntu/tomcat/webapps'
            }
        }

    }
}
