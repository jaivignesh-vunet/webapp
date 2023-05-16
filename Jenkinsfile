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
