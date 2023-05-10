pipeline {
    agent any

    stages {
        stage('git checkout') {
            steps {
                git branch: 'main', credentialsId: 'git-tocken', url: 'https://github.com/adminbala/hr-api'
            }
        }
        stage('maven build') {
            steps {
                sh 'mvn clean package'
            }
        }
         stage('tomcat deploy - dev') {
            steps {
                sshagent(['tomcat-dev']) {
                    sh "scp -o StrictHostKeyChecking=no target/hr-api.war ec2-user@172.31.37.102:/opt/tomcat9/webapps/"
                    sh "ssh ec2-user@172.31.37.102 /opt/tomcat9/bin/shutdown.sh"
                    sh "ssh ec2-user@172.31.37.102 /opt/tomcat9/bin/startup.sh"
                }
            }
        }
    }
}



