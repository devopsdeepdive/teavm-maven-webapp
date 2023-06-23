pipeline {
agent any
  stages {
  stage('Checkout') {
    steps {
      checkout scmGit(branches: [[name: '*/batch16']], extensions: [], userRemoteConfigs: [[credentialsId: 'github_passwd', url: 'https://github.com/devopsdeepdive/teavm-maven-webapp.git']])
    }
  }
     stage('Build') {
    steps {
      sh 'mvn compile'
    }
  }
     stage('Test') {
    steps {
      sh 'mvn test'
    }
  }
     stage('Package') {
    steps {
      sh 'mvn package'
    }
  }
      stage('Deploy') {
    steps {
     sshagent(['jenkins_agent']) {
   sh 'scp -o StrictHostKeyChecking=no /var/lib/jenkins/workspace/teavm-maven-webapp-pipeline/target/teavm-maven-webapp-1.1-SNAPSHOT.war ubuntu@172.31.23.42:/opt/tomcat/webapps'
}
}
    }
  } 
       
  }
