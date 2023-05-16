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
        withCredentials([usernamePassword(credentialsId: 'tomcat', usernameVariable: 'tomcatUsername', passwordVariable: 'tomcatPassword')]) {
            sh '''
              sshpass -p "${tomcatPassword}" scp -o StrictHostKeyChecking=no /var/lib/jenkins/workspace/webapp/target/WebApp.war ${tomcatUsername}@198.168.8.137:/opt/tomcat/webapps/webapp.war
            '''
        }
    }
}


    
  }
}
