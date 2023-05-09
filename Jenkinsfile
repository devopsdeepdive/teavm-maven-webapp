pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
				checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'github_cred', url: 'https://github.com/devopsdeepdive/teavm-maven-webapp.git']])            }
        }
        stage('Build') {
            steps {
				sh 'mvn compile'            }
        }
         stage('Test') {
            steps {
				sh 'mvn test'            }
        }
         stage('Package') {
            steps {
				sh 'mvn package'            }
        }
	     stage('Deploy') {
            steps {
		sshagent(['tomcat_server']) 
			 sh 'scp -o StrictHostKeyChecking=no  /var/lib/jenkins/workspace/teavm-maven-webapp-pipeline/target/teavm-maven-webapp-1.1-SNAPSHOT.war ubuntu@172.31.21.31/opt/tomcat/apache-tomcat-9.0.74/webapps'
		
	    }
        }
	     stage('Notify') {
            steps {
		slackSend channel: '#devopsdeepdive_batch15', message: 'Build successful'	    }
        }
    }
}
