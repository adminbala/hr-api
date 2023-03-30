pipeline {
    agent any

    stages {
        stage('Git Hub Pull') {
            steps {
                git branch: 'main', credentialsId: '7e6ca38b-aba6-4707-b26f-f3b344691e9d', url: 'https://github.com/benoynsreedhar/hr-api'
            }
        }
    }
}
