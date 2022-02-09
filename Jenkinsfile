pipeline{
agent any

stages{
	stage("git checkout"){
		steps{
		
		}
	}
	stage("maven build"){
		steps{
			sh "mvn clean package"
			sh "mv target/*.war target/webapp.war"
		}
	}
	stage("deploy"){
		steps{
			sshagent(['tomcat-new']) {
				sh "scp -o StrictHostKeyChecking=no target/webapp.war ec2-user@172.31.41.138:/opt/tomcat/webapps/"
			
				sh "ssh ec2-user@172.31.41.138 /opt/tomcat/bin/shutdown.sh"

				sh "ssh ec2-user@172.31.41.138 /opt/tomcat/bin/startup.sh"
			}
		}
	}
}
}
