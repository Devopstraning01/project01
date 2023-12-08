pipeline {
    agent any
    stages{
        stage("maven build"){
            steps{
                sh 'mvn package'
            }
        }
        stage("Dev Deploy"){
            steps{
                sshagent(['tomcat-dev']) {
                 // copy war file to tomcat dev server
                 sh "scp -o StrictHostKeyChecking=no target/project.war ec2-user@172.31.18.34:/opt/tomcat9/webapps/"
                 //restart tomcat server
                 sh "ssh ec2-user@172.31.18.34 /opt/tomcat9/bin/shutdown.sh"
                 sh "ssh ec2-user@172.31.18.34 /opt/tomcat9/bin/startup.sh"
                } 
            }
        }
    }
}
