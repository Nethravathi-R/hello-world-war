pipeline{
    agent { label 'java'}
    stages {
      stage ('checkout') {
        steps {
            sh 'rm -rf hello-world-war-Tomcat2'            
            sh 'git clone https://github.com/Nethravathi-R/Hello-world-war-Tomcat2.git'      
          
              }
      }
        stage ('build') {
        steps {
            sh 'mvn --version'
            sh 'mvn clean install'
              }
         }       
        stage ('deploy'){
            steps {
                sh 'ssh root@172.31.41.184'
                sh 'scp /home/slave1/jenkins/workspace/HelloWorldWar/target/hello-world-war-1.0.0.war root@172.31.41.184:/apache-tomcat-8.5.97/webapps'
            }
        }
    }
}
