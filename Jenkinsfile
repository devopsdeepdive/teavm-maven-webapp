pipeline {
agent any
  //agent {
  //label 'jenkins_slave'
//}
  stages {
  stage('Checkout') {
    steps {
      checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'github_cred', url: 'https://github.com/devopsdeepdive/teavm-maven-webapp.git']])
          sleep time: 1, unit: 'MINUTES'

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
     stage('Hello') {
    steps {
      sh 'echo "hello world"'
    }
  }
   /*   stage('Deploy') {
    steps {
      sshagent(['tomcat_deploy']) {
    sh 'scp -o StrictHostKeyChecking=no /var/lib/jenkins/workspace/teavm-maven-webapp-pipeline/target/teavm-maven-webapp-1.0-SNAPSHOT.war ubuntu@172.31.9.172:/opt/tomcat/webapps'
}
    }
  } */
     stage('Notify') {
      steps {
slackSend channel: '#devopsdeepdive_batch14', color: '#439FE0', message: 'message: "Build Started'      }
  }

}

}
