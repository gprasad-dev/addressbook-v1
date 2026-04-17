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
                step([$class: 'S3BucketPublisher', 
                    entries: [[
                        bucket: 'declarative-s3-bucket-jenkins', 
                        excludedFileMask: '', 
                        flatten: false, 
                        gzipFiles: false, 
                        managedArtifacts: false, 
                        noUploadOnFailure: true, 
                        selectedRegion: 'ap-south-1', 
                        showDirectlyInBrowser: false, 
                        sourceFile: 'target/addressbook.war', 
                        storageClass: 'STANDARD', 
                        uploadFromSlave: false, 
                        useServerSideEncryption: false
                    ]], 
                    profileName: 's3-profile-name', // MUST MATCH the name in Manage Jenkins -> System
                    dontWaitForConcurrentBuildCompletion: false, 
                    consoleLogPublishResult: true
                ])
            }
        }
    }
}
