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
			sh "mv target/*.war webapps/webapp.war"
		}
	}
	stage("deploy"){
		steps{
			sh "scp target/webapp.war tomcat@ipadress target/webapp.war"
			
			sh "ssh ec2-user@ipaddr /opt/tomcat/bin/shutdown.sh"

			sh "ssh ec2-user@ipaddr /opt/tomcat/bin/startup.sh"
		}

	}
}
}
