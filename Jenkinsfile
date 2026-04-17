pipeline {
    agent any

    stages {
        stage('git checkout') {
            steps {
                git credentialsId: 'cred-git', url: 'https://github.com/gprasad-dev/addressbook-v1.git'
            }
        }
        stage('compilation') {
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
                // This is the cleanest version that matches your plugin
                s3Upload(
                    profileName: 'S3-profile',
                    entries: [[
                        bucket: 'declarative-s3-bucket-jenkins',
                        sourceFile: 'target/addressbook.war',
                        selectedRegion: 'ap-south-1'
                    ]]
                )
            }
        }
    }
}
