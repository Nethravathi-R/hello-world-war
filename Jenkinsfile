pipeline{
    agent { label 'java'}
    stages {
      stage ('checkout') {
        steps {
            sh 'rm -rf hello-world-war'            
            sh 'git clone https://github.com/Nethravathi-R/hello-world-war.git'      
          
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
                sh 'scp /home/slave1/workspace/HelloWorldWar/target/hello-world-war-1.0.0.war root@172.31.41.184:/opt/apache-tomcat-8.5.98/webapps'
                
            }
        }
    }
}
