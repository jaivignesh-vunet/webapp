pipeline {

  agent any
  
  environment {
    EXAMPLE_CREDS = credentials('tomcat')
  }
  
  tools {
    maven 'Maven'
  }
  
  stages {
  
    stage ('Initialize') {
      steps {
        sh '''
                      echo "PATH = ${PATH}"
                      echo "M2_HOME = ${M2_HOME}"
             '''
      }
    }
    
    stage ('Check-Git-Secrets') {
      steps {
        sh 'rm trufflehog || true'
        sh 'docker run gesellix/trufflehog --json https://github.com/cehkunal/webapp.git > trufflehog'
        sh 'cat trufflehog'
      }
    }
    
    
    stage ('Build') {
      steps {
        sh 'mvn clean package'
      }
    }
    
    stage('Deploy-to-Tomcat') {
    steps {
        sh "sshpass -p 'tomcat' scp -o StrictHostKeyChecking=no /var/lib/jenkins/workspace/webapp/target/WebApp.war tomcat@192.168.8.137:/opt/tomcat/webapps/webapp.war"
    }
}


    
  }
}
