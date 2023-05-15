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
    
    stage('Deploy-to-Tomcat') {
      steps {
          withCredentials([usernamePassword(credentialsId: 'tomcat', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
              sh 'scp -o StrictHostKeyChecking=no target/*.war $USERNAME:$PASSWORD@198.168.1.7:/opt/tomcat/webapps/webapp.war'
          }
       }
    }
    
  }
}
