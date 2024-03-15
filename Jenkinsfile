pipeline{
    agent any
    stages {
      stage ('checkout') {
        steps {
            sh 'rm -rf hello-world-war'            
            sh 'git clone https://github.com/Nethravathi-R/hello-world-war.git'      
          
              }
      }
        stage ('build') {
        steps {
            sh 'echo inside build'
            dir("hello-world-war"){
                sh 'inside dir'
                sh 'docker build -t tomcat-war:1.0 .'
            }            
          }
         }       
        stage ('deploy'){
            steps {
               sh 'docker rm -f tomcat-war'
               sh 'docker run -d -p 8082:8080 --name tomcat-war tomcat-war:1.0'                
            }
        }
    }
}
