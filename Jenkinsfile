pipeline {
    agent any

    stages {
        stage('git checkout') {
            steps {
                git credentialsId: 'cred-git', url: 'https://github.com/gprasad-dev/addressbook-v1.git'
            }
        }
    }
}
