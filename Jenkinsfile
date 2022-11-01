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
    stage ('Deploy-To-Tomcat') {
            steps {
           sshagent(['tomcat']) {
                sh 'scp -o StrictHostKeyChecking=no target/*.war ubuntu@44.201.87.156:/home/ubuntu/prod/apache-tomcat-9.0.68/webapps/webapp.war'
              }      
           }       
        }
  }
}
