pipeline {
    agent any
    
    stages {
        stage('Git-Checkout') {
            steps {
                git branch: 'main', credentialsId: 'crds', url: 'https://github.com/benoynsreedhar/hr-api'
             }
        }
        stage('Maven-Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Tomcat-Deploy') {
            steps {
                sshagent(['tomcat-creds']) {
                    sh"scp -o StrictHostKeyChecking=no target/*.war ec2-user@172.31.89.251:/opt/tomcat9/webapps"
                    sh"ssh ec2-user@172.31.89.251 /opt/tomcat9/bin/shutdown.sh"
                    sh"ssh ec2-user@172.31.89.251 /opt/tomcat9/bin/startup.sh"
               }
            }
        }
    }
    post {
          always {
            cleanWs()
          }
        }
}
