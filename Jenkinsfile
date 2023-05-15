pipeline {

  agent any

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
    
    stage ('Build') {
      steps {
        sh 'mvn clean package'
      }
    }
    
    stage ('Deploy-to-Tomcat') {
      steps {
            sh 'scp -o StrictHostKeyChecking=no target/*.war tomcat:tomcat@198.168.1.7:/opt/tomcat/webapps/webapp.war'
      }
    }
    
  }
}
