pipeline{
agent any

stages{
	stage("git checkout"){
		steps{
			git branch: 'main', credentialsId: 'gituser', url: 'https://github.com/vinayakanu/super.git'
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
			
				sh "ssh ec2-user@172.31.41.138 /tmp/tomcatstop.sh"

				sh "ssh ec2-user@172.31.41.138 /tmp/tomcatstart.sh"
			}
		}
	}
}
}
