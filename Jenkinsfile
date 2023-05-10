@Library('jhc') _ 
pipeline {
    agent any
    stages {
        stage('git checkout') {
            when{
                expression{
                    params.branchname == "develop"
                }
            }
            steps {
               git branch: "${params.branchname}", credentialsId: 'git-tocken', url: 'https://github.com/adminbala/hr-api'
            }
        }
        stage('maven build') {
             when{
                expression{
                    params.branchname == "develop"
                }
            }
            steps {
                sh 'mvn clean package'
            }
        }   
        stage('tomcat deploy - dev') {
            steps {
               tomcatDeploy() 
            }
        } 
    }
    post {
  always {
    cleanWs()
  }
 }
}

