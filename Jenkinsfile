pipeline {
    agent any
    environment {
        PATH = "/opt/maven/bin:$PATH"
    }
    stages {
        stage("clone code"){
            steps{
               git credentialsId: 'git_credentials', url: 'https://github.com/devopslord/jenkins-tomcat.git'
            }
        }
        stage("build code"){
            steps{
              sh "mvn clean install"
            }
        }
        stage("deploy to tocat"){
            steps{
              sshagent(['deploy-user']) {
                 sh "scp -o StrictHostKeyChecking=no webapp/target/webapp.war ec2-user@3.83.251.66:/opt/tomcat/webapps"
                 
                }
            }
        }
    }
}
