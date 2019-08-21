pipeline {
    agent any

	tools {
		maven 'maven3.6'
	}

//	environment {
//		M2_INSTALL = "/home/gamut/Distros/apache-maven-3.6.0/bin/mvn"
//	}

    stages {
		stage('Clone-Repo') {
			steps {
				checkout scm
			}
		}
		stage('Build') {
	    	steps {
				sh 'mvn install -DskipTests'
			}
	    }
		stage('Unit Tests') {
			steps {
				sh 'mvn surefire:test'
			}
		}
		stage('Deployment') {
	    	steps {
				sh 'sshpass -p "gamut" scp target/gamutkart.war lakshmi@172.17.0.2:/home/lakshmi/Distros/apache-tomcat-8.5.38/webapps'
				sh 'sshpass -p "gamut" ssh lakshmi@172.17.0.2 "JAVA_HOME=/home/lakshmi/Distros/jdk1.8.0_151" "/home/lakshmi/Distros/apache-tomcat-8.5.38/bin/startup.sh"'
	    	}
		}
    }
}
